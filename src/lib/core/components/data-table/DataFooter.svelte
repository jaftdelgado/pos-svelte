<script lang="ts">
	import type { Table } from '@tanstack/table-core';
	import Button from '$lib/core/ui/Button.svelte';

	let { table }: { table: Table<any> } = $props();
</script>

<div class="flex items-center justify-between px-2 py-1">
	<div class="text-sm text-gray-500">
		Mostrando <span class="font-medium">{table.getRowModel().rows.length}</span> de
		<span class="font-medium">{table.getCoreRowModel().rows.length}</span> registros
	</div>

	<div class="flex items-center gap-4">
		<span class="text-sm text-gray-500">
			Página {table.getState().pagination.pageIndex + 1} de {table.getPageCount()}
		</span>
		<div class="flex gap-2">
			<Button
				variant="outline"
				size="sm"
				onclick={() => table.previousPage()}
				disabled={!table.getCanPreviousPage()}
			>
				Anterior
			</Button>
			<Button
				variant="outline"
				size="sm"
				onclick={() => table.nextPage()}
				disabled={!table.getCanNextPage()}
			>
				Siguiente
			</Button>
		</div>
	</div>
</div>