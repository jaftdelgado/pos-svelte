<script lang="ts">
	import type { HeaderGroup } from '@tanstack/table-core';

	let { headerGroup }: { headerGroup: HeaderGroup<any> } = $props();
</script>

<thead class="border-b border-gray-200 bg-gray-50">
	<tr>
		{#each headerGroup.headers as header}
			<th
				class="border-gray-200 cursor-pointer select-none px-4 h-control-xl font-medium text-secondaryText transition-colors border-r hover:bg-gray-100 last:border-r-0"
				onclick={header.column.getToggleSortingHandler()}
			>
				<div class="flex items-center gap-2">
					{#if !header.isPlaceholder}
						{header.column.columnDef.header}
						{#if header.column.getIsSorted() === 'asc'}
							<span class="text-xs">▲</span>
						{:else if header.column.getIsSorted() === 'desc'}
							<span class="text-xs">▼</span>
						{/if}
					{/if}
				</div>
			</th>
		{/each}
	</tr>
</thead>