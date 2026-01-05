<script lang="ts">
	import type { Snippet } from 'svelte';

	let { 
		title, 
		subtitle, 
		actions 
	}: { 
		title: string; 
		subtitle?: string; 
		actions?: Snippet 
	} = $props();
</script>

<header class="flex flex-col gap-4 sm:flex-row sm:items-center sm:justify-between px-1 py-6">
	<div class="flex flex-col gap-1">
		<h1 class="text-xl font-semibold tracking-tight text-gray-900 sm:text-3xl">
			{title}
		</h1>
		{#if subtitle}
			<p class="text-secondaryText">
				{subtitle}
			</p>
		{/if}
	</div>

	{#if actions}
		<div class="flex items-center gap-3">
			{@render actions()}
		</div>
	{/if}
</header>