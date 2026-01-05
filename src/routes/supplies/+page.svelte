<script lang="ts">
	import Button from '$lib/core/ui/Button.svelte';
	import DataTable from '$lib/core/components/data-table/DataTable.svelte';
	import PageHeader from '$lib/core/components/PageHeader.svelte';

	const supplies = [
		{ id: 1, name: 'Harina de Trigo', unit: 'kg', quantity: 100, minStock: 20 },
		{ id: 2, name: 'Aceite Vegetal', unit: 'Lts', quantity: 45, minStock: 10 },
		{ id: 3, name: 'Azúcar Refinada', unit: 'kg', quantity: 30, minStock: 5 },
		{ id: 4, name: 'Sal Industrial', unit: 'kg', quantity: 10, minStock: 2 }
	];

	const columns = [
		{ accessorKey: 'name', header: 'Insumo' },
		{ accessorKey: 'unit', header: 'Unidad' },
		{ accessorKey: 'quantity', header: 'Cantidad Actual' },
		{ 
			accessorKey: 'minStock', 
			header: 'Stock Mínimo',
			cell: (info: any) => {
				const val = info.getValue();
				return val;
			}
		}
	];
</script>

<div class="mx-auto w-full px-14">
	<PageHeader 
		title="Gestión de Insumos" 
		subtitle="Control de materias primas y recursos para producción">
		{#snippet actions()}
			<Button variant="outline">Reporte de Faltantes</Button>
			<Button variant="default">Registrar Entrada</Button>
		{/snippet}
	</PageHeader>

	<div class="mt-8">
		<DataTable data={supplies} {columns} />
	</div>
</div>