<script lang="ts">
	import Button from '$lib/core/ui/Button.svelte';
	import DataTable from '$lib/core/components/data-table/DataTable.svelte';
	import PageHeader from '$lib/core/components/PageHeader.svelte';

	const products = [
		{ id: 1, name: 'Coca Cola', category: 'Bebidas', price: 15.5, stock: 50 },
		{ id: 2, name: 'Papas Fritas', category: 'Snacks', price: 12.0, stock: 20 },
		{ id: 3, name: 'Leche Entera', category: 'Lácteos', price: 24.0, stock: 15 },
		{ id: 4, name: 'Pan Blanco', category: 'Panadería', price: 35.0, stock: 10 },
		{ id: 5, name: 'Jabón de Manos', category: 'Limpieza', price: 18.0, stock: 100 },
		{ id: 6, name: 'Detergente', category: 'Limpieza', price: 45.0, stock: 5 }
	];

	const columns = [
		{ accessorKey: 'name', header: 'Producto' },
		{ accessorKey: 'category', header: 'Categoría' },
		{
			accessorKey: 'price',
			header: 'Precio',
			cell: (info: any) => `$${info.getValue().toFixed(2)}`
		},
		{ accessorKey: 'stock', header: 'Existencias' }
	];
</script>

<div class="mx-auto w-full max-w-6xl p-6">
	<PageHeader 
		title="Inventario de Productos" 
		subtitle="Listado general de existencias y precios por categoría">
		{#snippet actions()}
			<Button variant="outline">Exportar</Button>
			<Button variant="default">Nuevo Producto</Button>
		{/snippet}
	</PageHeader>

	<div class="mt-8">
		<DataTable data={products} {columns} />
	</div>
</div>