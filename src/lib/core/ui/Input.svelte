<script lang="ts">
	import { cn } from '$lib/core/utils/cn';
	import type { HTMLInputAttributes } from 'svelte/elements';
	import type { Snippet } from 'svelte';

	type InputSize = 'sm' | 'md' | 'lg';

	interface Props extends Omit<HTMLInputAttributes, 'size'> {
		size?: InputSize;
		startContent?: Snippet;
		endContent?: Snippet;
	}

	let { 
		size = 'md', 
		class: className, 
		startContent, 
		endContent, 
		...rest 
	}: Props = $props();

	const sizes = {
		sm: 'h-control-sm px-3',
		md: 'h-control-md px-3',
		lg: 'h-control-lg px-4'
	};

	const baseStyles =
		'flex w-full items-center gap-2 border border-outline bg-white rounded-control transition-all text-text-primary focus-within:ring-1 focus-within:ring-control-primary focus-within:border-control-primary disabled:cursor-not-allowed disabled:opacity-50';
</script>

<div class={cn(baseStyles, sizes[size], className)}>
	{#if startContent}
		<div class="flex items-center justify-center text-text-tertiary">
			{@render startContent()}
		</div>
	{/if}

	<input
		class="w-full bg-transparent border-none p-0 outline-none ring-0 focus:ring-0 placeholder:text-text-tertiary disabled:cursor-not-allowed"
		{...rest}
	/>

	{#if endContent}
		<div class="flex items-center justify-center text-text-tertiary">
			{@render endContent()}
		</div>
	{/if}
</div>