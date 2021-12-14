<script>
	let board = new Set();
	const I_9 = [[1, 0, 0, 0, 0, 0, 0, 0, 0],
			[0, 1, 0, 0, 0, 0, 0, 0, 0],
			[0, 0, 1, 0, 0, 0, 0, 0, 0],
			[0, 0, 0, 1, 0, 0, 0, 0, 0],
			[0, 0, 0, 0, 1, 0, 0, 0, 0],
			[0, 0, 0, 0, 0, 1, 0, 0, 0],
			[0, 0, 0, 0, 0, 0, 1, 0, 0],
			[0, 0, 0, 0, 0, 0, 0, 1, 0],
			[0, 0, 0, 0, 0, 0, 0, 0, 1]
	];

	function create_permutation(starting_matrix) {
		let permutation = [];
		for (let i = 0; i < starting_matrix.length; i++) {
			let row = Math.floor(Math.random() * starting_matrix.length);

			if (row in starting_matrix) {
				permutation.push(starting_matrix[row]);
				starting_matrix.splice(row, 1);
			}
		}
		return permutation;
	}

	while (board.size < 9) {
		board.add(create_permutation(I_9));
	}

	let blanks = [];
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
							{board[9 * i + j]}
						{/if}
					</td>
					{#if ((j+1) % 3 == 0)}
						<span class="vertical-bar"></span>
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
		width: 1rem;
	}
	.horizontal-bar {
		height: 1rem;
	}
</style>
