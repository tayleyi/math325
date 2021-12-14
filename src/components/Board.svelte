<script>
	import * as math from 'mathjs';

	export let easy;
	let board = [];

	function create_permutation() {
		let starting_matrix = math.identity(9);

		let tmp = [];
		let p = [];

		for (let i = 0; i < 9; i++) {
			tmp.push(math.row(starting_matrix, i));
		}

		for (let i = 0; i < 9; i++) {
			let row_number = Math.floor(Math.random() * tmp.length);
			p.push(tmp[row_number]);
			tmp.splice(row_number, 1);
		}

		let permutation = math.matrixFromRows(
			p[0], p[1], p[2],
			p[3], p[4], p[5],
			p[6], p[7], p[8]
		);
		return permutation;
	}

	while (board.length < 9) {
		board.push(create_permutation());
	}
	let current_game = math.zeros(9, 9);
	for (let i = 0; i < board.length; i++) {
		let ith_row = math.multiply(i + 1, board[i]);
		current_game = math.add(current_game, ith_row);
	}
	let blanks = [];
	if (easy) {
		upperLimit = 20;
	}
	else {
		upperLimit = 40;
	}
	for (let k = 0; k < upperLimit; k++) {
		blanks.push(Math.floor(Math.random() * 81 + 1));
	}
</script>

<div>
	<h1>sudoku</h1>
	<table>
		{#each {length: 9} as _, i}
			<tr>
				{#each {length: 9} as _, j}
					<td>
						{#if blanks.includes(9 * i + j)}
							<input>
						{:else}
							{current_game.get([i, j])}
						{/if}
					</td>
					{#if ((j+1) % 3 == 0)}
						<td class="vertical-bar"></td>
					{/if}
				{/each}
			</tr>
			{#if ((i+1) % 3 == 0)}
				<tr class="horizontal-bar"></tr>
			{/if}
		{/each}
	</table>
</div>

<style>
	table {
		margin-right: auto;
		margin-left: auto;
		width: 80%;
		height: 80%;
	}
	tr, td {
		border: solid;
	}
	table {
		width: 30rem;
	}
	input, td, tr {
		width: 2rem;
		height: 2rem;
	}
	.vertical-bar {
		width: .5rem;
		border: none;
	}
	.horizontal-bar {
		height: 1rem;
	}
</style>
