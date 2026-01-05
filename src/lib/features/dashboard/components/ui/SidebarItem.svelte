<script lang="ts">
    import { cn } from '$lib/core/utils/cn';
    import type { Snippet } from 'svelte';

    interface Props {
        label: string;
        active?: boolean;
        isCollapsed?: boolean;
        icon?: Snippet;
        children?: Snippet;
        onclick?: () => void;
    }

    let { 
        label, 
        active = false, 
        isCollapsed = false, 
        icon, 
        children,
        onclick 
    }: Props = $props();
</script>

<button 
    {onclick}
    class={cn(
        "w-full flex items-center gap-3 p-3 rounded-control transition-all group overflow-hidden",
        active 
            ? "bg-control-primary text-white" 
            : "hover:bg-white/5 text-text-tertiary hover:text-text-primary"
    )}
    title={isCollapsed ? label : undefined}
>
    <div class="shrink-0">
        {#if icon}
            {@render icon()}
        {:else if children}
            {@render children()} {:else}
            <div class="w-5 h-5 border-2 border-current rounded-sm opacity-80 group-hover:opacity-100"></div>
        {/if}
    </div>

    {#if !isCollapsed}
        <span class="font-medium text-body whitespace-nowrap">
            {label}
        </span>
    {/if}
</button>