<script lang="ts">
	import './layout.css';
	import AppSidebar from '$lib/features/dashboard/components/AppSidebar.svelte';

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href="/favicon.png" />
</svelte:head>

<div class="flex h-screen w-full overflow-hidden bg-white">
	<AppSidebar />

	<main class="flex-1 overflow-y-auto scroll-container">
		{@render children()}
	</main>
</div>