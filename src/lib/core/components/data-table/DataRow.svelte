<script lang="ts">
	import type { Row } from '@tanstack/table-core';

	let { row }: { row: Row<any> } = $props();
</script>

<tr class="transition-colors hover:bg-gray-50">
	{#each row.getVisibleCells() as cell}
		<td class="border-gray-200 px-4 h-control-xl text-gray-600 border-r last:border-r-0">
			{cell.getValue()}
		</td>
	{/each}
</tr>