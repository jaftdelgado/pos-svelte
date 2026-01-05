<script lang="ts">
    import { cn } from '$lib/core/utils/cn';
    import Button from '$lib/core/ui/Button.svelte';
    import SidebarItem from './ui/SidebarItem.svelte';
    import ReservationIcon from '$lib/features/dashboard/resources/svg/ReservationsIcon.svelte'; 

    let isCollapsed = $state(false);
    let activeRoute = $state('Dashboard');

    const menuItems = [
        { label: 'Dashboard' },
        { label: 'Reservaciones', icon: ReservationIcon }, 
        { label: 'Ventas' },
        { label: 'Inventario' },
        { label: 'Clientes' },
        { label: 'Reportes' }
    ];
</script>

<aside 
    class={cn(
        "flex flex-col h-screen bg-slate-100 text-white transition-all duration-300 border-r border-outline-strong",
        isCollapsed ? "w-20" : "w-64"
    )}
>
    <div class="flex items-center justify-between p-4 h-control-lg overflow-hidden">
        {#if !isCollapsed}
            <span class="font-bold text-lg tracking-tight px-2 whitespace-nowrap text-white">NEXUS POS</span>
        {/if}
        <button 
            onclick={() => isCollapsed = !isCollapsed} 
            class="p-2 hover:bg-white/10 rounded-control transition-colors mx-auto shrink-0"
            aria-label={isCollapsed ? "Expandir menú" : "Colapsar menú"}
            title={isCollapsed ? "Expandir" : "Colapsar"}
        >
            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                <rect width="18" height="18" x="3" y="3" rx="2"/><path d="M9 3v18"/>
            </svg>
        </button>
    </div>

    <nav class="flex-1 px-3 py-4 space-y-2">
        {#each menuItems as item}
            <SidebarItem 
                label={item.label} 
                active={activeRoute === item.label}
                {isCollapsed}
                onclick={() => activeRoute = item.label}
            >
                {#if item.icon}
                    <item.icon size={18} />
                {/if}
            </SidebarItem>
        {/each}
    </nav>

    <div class="p-4 border-t border-white/10 overflow-hidden">
        <Button 
            variant="ghost" 
            class={cn(
                "w-full text-white/70 hover:text-white hover:bg-red-500/20",
                isCollapsed ? "justify-center px-0" : "justify-start px-2"
            )}
            size="sm"
            aria-label="Cerrar sesión"
        >
            <div class="w-5 h-5 border-2 border-current rounded-sm shrink-0"></div>
            {#if !isCollapsed}
                <span class="whitespace-nowrap">Cerrar Sesión</span>
            {/if}
        </Button>
    </div>
</aside>