<script lang="ts">
	import Button from '$lib/core/ui/Button.svelte';
	import Input from '$lib/core/ui/Input.svelte'; // Línea generada
</script>

<div class="flex min-h-screen flex-col items-center justify-center gap-8 p-4">
	<div class="text-center">
		<h1 class="text-3xl font-bold">POS System</h1>
		<p class="text-gray-600">Componentes core con tokens de diseño</p>
	</div>

	<div class="flex flex-wrap items-center gap-4 border-t pt-6">
		<Button variant="default" size="lg">Nueva Venta</Button>
		<Button variant="secondary">Inventario</Button>
		<Button variant="outline" size="sm">Configuración</Button>
		<Button variant="ghost" class="text-red-500 hover:text-red-700">Cerrar Sesión</Button>
	</div>

	<div class="flex w-full max-w-2xl flex-col gap-4 border-t pt-6">
		<div class="flex items-center gap-4">
			<Input size="lg" placeholder="Buscador grande (lg)..." class="flex-1" />
			<Button size="lg">Buscar</Button>
		</div>

		<div class="flex items-center gap-4">
			<Input size="md" placeholder="Input estándar (md)..." class="flex-1" />
			<Button variant="secondary" size="md">Escanear</Button>
		</div>

		<div class="flex items-center gap-4">
			<Input size="sm" placeholder="Input pequeño (sm)..." class="flex-1" />
			<Button variant="outline" size="sm">Aplicar</Button>
		</div>
	</div>
</div>