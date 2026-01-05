<script lang="ts">
	import {
		createTable,
		getCoreRowModel,
		getSortedRowModel,
		getPaginationRowModel,
		getFilteredRowModel,
		type TableState,
		type ColumnDef,
		type Updater
	} from '@tanstack/table-core';
	import Input from '$lib/core/ui/Input.svelte';
	import DataRow from './DataRow.svelte';
	import DataHeader from './DataHeader.svelte';
	import DataFooter from './DataFooter.svelte';

	let { data, columns }: { data: any[]; columns: ColumnDef<any, any>[] } = $props();

	let state = $state<Partial<TableState>>({
		sorting: [],
		pagination: { pageIndex: 0, pageSize: 5 },
		columnFilters: [],
		globalFilter: '',
		columnVisibility: {},
		columnOrder: [],
		columnPinning: {},
		rowSelection: {},
		columnSizing: {},
		columnSizingInfo: {} as any
	});

	const table = createTable({
		get data() { return data; },
		get columns() { return columns; },
		state: {
			get sorting() { return state.sorting; },
			get pagination() { return state.pagination; },
			get columnFilters() { return state.columnFilters; },
			get globalFilter() { return state.globalFilter; },
			get columnVisibility() { return state.columnVisibility; },
			get columnOrder() { return state.columnOrder; },
			get columnPinning() { return state.columnPinning; },
			get rowSelection() { return state.rowSelection; },
			get columnSizing() { return state.columnSizing; },
			get columnSizingInfo() { return state.columnSizingInfo; }
		},
		onStateChange: (updater: Updater<any>) => {
			if (typeof updater === 'function') {
				state = updater(state as TableState);
			} else {
				state = updater;
			}
		},
		getCoreRowModel: getCoreRowModel(),
		getSortedRowModel: getSortedRowModel(),
		getPaginationRowModel: getPaginationRowModel(),
		getFilteredRowModel: getFilteredRowModel(),
		renderFallbackValue: null
	});
</script>

<div class="flex w-full flex-col gap-4">
	<div class="flex items-center justify-between gap-4">
		<Input
			placeholder="Buscar en todos los campos..."
			value={state.globalFilter ?? ''}
			oninput={(e) => table.setGlobalFilter(e.currentTarget.value)}
			class="max-w-sm"
		/>
	</div>

	<div class="overflow-hidden rounded-lg border border-gray-200 bg-white">
		<table class="w-full border-collapse text-left text-sm">
			{#each table.getHeaderGroups() as headerGroup}
				<DataHeader {headerGroup} />
			{/each}
			
			<tbody class="divide-y divide-gray-200">
				{#each table.getRowModel().rows as row}
					<DataRow {row} />
				{/each}

				{#if table.getRowModel().rows.length === 0}
					<tr>
						<td colspan={columns.length} class="px-4 py-8 text-center italic text-gray-400">
							No se encontraron resultados.
						</td>
					</tr>
				{/if}
			</tbody>
		</table>
	</div>

	<DataFooter {table} />
</div>