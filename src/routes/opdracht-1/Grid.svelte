<script lang="ts">
	import { createEventDispatcher } from 'svelte';
	import type { GridData } from './utils';

	export let digits: GridData;

	const dispatch = createEventDispatcher();
	function onClick(x: number, y: number) {
		dispatch('click', { x, y });
	}
</script>

<table class="digits">
	{#each Array(digits.size) as _, y (y)}
		<tr>
			{#each Array(digits.size) as _, x (x)}
				<td class="digit" class:active={digits.get(x, y) === 1} on:click={() => onClick(x, y)}></td>
			{/each}
		</tr>
	{/each}
</table>

<style lang="postcss">
	.digits {
		border-collapse: collapse;

		& td,
		th {
			border: 1px solid black;
		}
	}

	.digit {
		width: 1em;
		height: 1em;
		text-align: center;
		background-color: white;

		&.active {
			background-color: black;
		}
	}
</style>
