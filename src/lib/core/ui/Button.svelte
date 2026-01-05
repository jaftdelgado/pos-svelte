<script lang="ts">
	import { cn } from '$lib/core/utils/cn';
	import type { HTMLButtonAttributes } from 'svelte/elements';
	import type { Snippet } from 'svelte';

	type ButtonVariant = 'default' | 'secondary' | 'outline' | 'ghost';
	type ButtonSize = 'sm' | 'md' | 'lg';

	interface Props extends HTMLButtonAttributes {
		variant?: ButtonVariant;
		size?: ButtonSize;
		children?: Snippet;
		startContent?: Snippet;
		endContent?: Snippet;
	}

	let { 
		variant = 'default', 
		size = 'md', 
		class: className, 
		children, 
		startContent, 
		endContent, 
		...rest 
	}: Props = $props();

	const variants = {
		default: 'bg-control-primary text-white hover:bg-control-primary-hover shadow active:scale-[0.98]',
		secondary: 'bg-control-secondary text-white hover:bg-control-secondary-hover active:scale-[0.98]',
		outline: 'border border-outline-strong bg-transparent hover:bg-slate-50 text-text-secondary',
		ghost: 'bg-transparent hover:bg-slate-50 text-text-primary'
	};

	const sizes = {
		sm: 'h-control-sm px-3',
		md: 'h-control-md px-4',
		lg: 'h-control-lg px-5'
	};

	const baseStyles =
		'inline-flex items-center justify-center gap-2 whitespace-nowrap rounded-control font-medium transition-all focus-visible:outline-none focus-visible:ring-1 focus-visible:ring-control-primary disabled:pointer-events-none disabled:opacity-50 leading-none';
</script>

<button 
	class={cn(baseStyles, sizes[size], variants[variant], className)} 
	{...rest}
>
	{#if startContent}
		{@render startContent()}
	{/if}

	{#if children}
		{@render children()}
	{/if}

	{#if endContent}
		{@render endContent()}
	{/if}
</button>