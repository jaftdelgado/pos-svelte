<script lang="ts">
	import { cn } from '$lib/core/utils/cn';
	import { goto } from '$app/navigation';
	import { page } from '$app/state';
	import Button from '$lib/core/ui/Button.svelte';
	import SidebarItem from './ui/SidebarItem.svelte';
	import ReservationIcon from '$lib/features/dashboard/resources/svg/ReservationsIcon.svelte';

	let isCollapsed = $state(false);

	const menuItems = [
		{ label: 'Dashboard', href: '/dashboard' },
		{ label: 'Reservaciones', href: '/reservations', icon: ReservationIcon },
		{ label: 'Ventas', href: '/sales' },
        { label: 'Insumos', href: '/supplies' },
		{ label: 'Inventario', href: '/inventory' },
		{ label: 'Clientes', href: '/customers' },
		{ label: 'Reportes', href: '/reports' }
	];

	let activeRoute = $derived(page.url.pathname);
</script>

<aside
	class={cn(
		"flex h-screen flex-col border-r border-outline-strong bg-slate-100 transition-all duration-300",
		isCollapsed ? "w-20" : "w-64"
	)}
>
	<div class="h-control-lg flex items-center justify-between overflow-hidden p-4">
		{#if !isCollapsed}
			<span class="whitespace-nowrap px-2 text-lg font-bold tracking-tight text-slate-900">
				NEXUS POS
			</span>
		{/if}
		<button
			onclick={() => (isCollapsed = !isCollapsed)}
			class="mx-auto shrink-0 rounded-control p-2 text-slate-600 transition-colors hover:bg-black/5"
			aria-label={isCollapsed ? "Expandir menú" : "Colapsar menú"}
			title={isCollapsed ? "Expandir" : "Colapsar"}
		>
			<svg
				xmlns="http://www.w3.org/2000/svg"
				width="20"
				height="20"
				viewBox="0 0 24 24"
				fill="none"
				stroke="currentColor"
				stroke-width="2"
				stroke-linecap="round"
				stroke-linejoin="round"
			>
				<rect width="18" height="18" x="3" y="3" rx="2" /><path d="M9 3v18" />
			</svg>
		</button>
	</div>

	<nav class="flex-1 space-y-2 px-3 py-4">
		{#each menuItems as item}
			<SidebarItem
				label={item.label}
				active={activeRoute === item.href}
				{isCollapsed}
				onclick={() => goto(item.href)}
			>
				{#if item.icon}
					<item.icon size={18} />
				{/if}
			</SidebarItem>
		{/each}
	</nav>

	<div class="overflow-hidden border-t border-black/5 p-4">
		<button
			class={cn(
				"flex items-center gap-3 rounded-control p-3 transition-all hover:bg-red-50 text-slate-600 hover:text-red-600 w-full",
				isCollapsed ? "justify-center" : "justify-start"
			)}
			onclick={() => goto('/logout')}
			aria-label="Cerrar sesión"
		>
			<div class="h-5 w-5 shrink-0 border-2 border-current rounded-sm"></div>
			{#if !isCollapsed}
				<span class="whitespace-nowrap font-medium">Cerrar Sesión</span>
			{/if}
		</button>
	</div>
</aside>