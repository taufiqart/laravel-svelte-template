<script>
  import { Link, useForm } from '@inertiajs/svelte';
  import GuestLayout from '@/layouts/guest-layout.svelte';
  import InputError from '@/components/input-error.svelte';

  import { Label } from '@/components/ui/label/index.js';
  import { Button } from '@/components/ui/button/index.js';
  import { Input } from '@/components/ui/input/index.js';
  import { Checkbox } from '@/components/ui/checkbox/index.js';

  let { canResetPassword, status } = $props();

  const form = useForm({
    email: '',
    password: '',
    remember: false,
  });

  const submit = (e) => {
    e.preventDefault();
    $form.post(route('login'));
  };
</script>

<GuestLayout>
  {#if status}
    <div class="mb-4 text-sm font-medium text-green-600">
      {status}
    </div>
  {/if}

  <form onsubmit={submit} class="flex flex-col gap-4 py-4">
    <div class="flex flex-col gap-1">
      <Label for="email">Email</Label>

      <Input
        id="email"
        type="email"
        bind:value={$form.email}
        class="mt-1 block w-full"
        required
        autofocus
        autocomplete="username"
      />

      <InputError class="mt-2" message={$form.errors.email} />
    </div>

    <div class="flex flex-col gap-1">
      <Label for="password">Password</Label>

      <Input
        id="password"
        type="password"
        bind:value={$form.password}
        class="mt-1 block w-full"
        required
        autocomplete="current-password"
      />

      <InputError class="mt-2" message={$form.errors.password} />
    </div>

    <div class="flex flex-col gap-1">
      <label class="flex items-center">
        <Checkbox bind:checked={$form.remember} />
        <span class="ms-2 text-sm text-gray-600 dark:text-gray-400"> Remember me </span>
      </label>
    </div>

    <div class="mt-4 flex items-center justify-end gap-1">
      {#if canResetPassword}
        <Link
          href={route('password.request')}
          class="rounded-md text-sm text-gray-600 underline hover:text-gray-900 focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 focus:outline-none dark:text-gray-400 dark:hover:text-gray-100 dark:focus:ring-offset-gray-800"
        >
          Forgot your password?
        </Link>
      {/if}

      <Button
        type="submit"
        class={'ms-4' + ($form.processing ? 'opacity-25' : '')}
        disabled={$form.processing}
      >
        Log in
      </Button>
    </div>
  </form>
</GuestLayout>
