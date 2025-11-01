<script>
    import { Toaster } from "@/components/ui/sonner/index.js";

    let { children } = $props();
</script>

<Toaster position="top-right" />
{@render children?.()}
