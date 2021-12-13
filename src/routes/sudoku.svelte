<script>
	import { onMount } from 'svelte';
	import Board from './Board.svelte';

	let easy = true;

	if (easy) {

	}


	let startTime = new Date();
	let time = new Date();
	$: minutes = new Date(time - startTime).getMinutes();
	$: seconds = new Date(time - startTime).getSeconds();
	onMount(() => {
		const interval = setInterval(() => {
			time = new Date();
		}, 1000);
	});
</script>

<main>
	<Board easy={easy} />

	<div class="status-box">
		<p class="time-elapsed">{minutes}:{(seconds < 10) ? '0' + seconds : seconds}</p>
		<div class="difficulty-setting">
			<label>
				<input type=radio bind:group={easy} name="difficulty" value={true}>
				easy
			</label>
			<label>
				<input type=radio bind:group={easy} name="difficulty" value={false}>
				difficult
			</label>
		</div>
		<button>status update</button>
	</div>
</main>

<style>
	main {
		text-align: center;
		width: 80vw;
		margin-left: 10%;
		margin-right: 10%;
		font-size: 28px;
	}
	.status-box {
		display: flex;
		flex-direction: row;
	}
	.difficulty-setting {
		flex: 1;
	}
	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
