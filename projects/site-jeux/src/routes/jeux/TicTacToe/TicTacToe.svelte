<script>
	import Tile from './Tile.svelte'
	export let clicks = 0
	let gameOver = false

	function checkGrid() {
		if (
			symbols[0] + symbols[1] + symbols[2] === 'XXX' ||
			symbols[0] + symbols[1] + symbols[2] === 'OOO' ||
			symbols[3] + symbols[4] + symbols[5] === 'XXX' ||
			symbols[3] + symbols[4] + symbols[5] === 'OOO' ||
			symbols[6] + symbols[7] + symbols[8] === 'XXX' ||
			symbols[6] + symbols[7] + symbols[8] === 'OOO' ||
			symbols[0] + symbols[3] + symbols[6] === 'XXX' ||
			symbols[0] + symbols[3] + symbols[6] === 'OOO' ||
			symbols[1] + symbols[4] + symbols[7] === 'XXX' ||
			symbols[1] + symbols[4] + symbols[7] === 'OOO' ||
			symbols[2] + symbols[5] + symbols[8] === 'XXX' ||
			symbols[2] + symbols[5] + symbols[8] === 'OOO' ||
			symbols[0] + symbols[4] + symbols[8] === 'XXX' ||
			symbols[0] + symbols[4] + symbols[8] === 'OOO' ||
			symbols[2] + symbols[4] + symbols[6] === 'XXX' ||
			symbols[2] + symbols[4] + symbols[6] === 'OOO'
		) {
			gameOver = true
		}
	}

	const symbols = ['', '', '', '', '', '', '', '', '']

	function setSymbol(i) {
		console.log('setSymbol')
		if (symbols[i] === '' && !gameOver) {
			clicks++
			console.log('clicks', clicks)
			symbols[i] = clicks % 2 === 0 ? 'X' : 'O'
		}
		checkGrid()
	}
</script>

<div class="flex flex-col items-center">
	<div class="w-max grid grid-cols-3 gap-4 my-6">
		<Tile on:click={() => setSymbol(0)} symbol={symbols[0]} />
		<Tile on:click={() => setSymbol(1)} symbol={symbols[1]} />
		<Tile on:click={() => setSymbol(2)} symbol={symbols[2]} />
		<Tile on:click={() => setSymbol(3)} symbol={symbols[3]} />
		<Tile on:click={() => setSymbol(4)} symbol={symbols[4]} />
		<Tile on:click={() => setSymbol(5)} symbol={symbols[5]} />
		<Tile on:click={() => setSymbol(6)} symbol={symbols[6]} />
		<Tile on:click={() => setSymbol(7)} symbol={symbols[7]} />
		<Tile on:click={() => setSymbol(8)} symbol={symbols[8]} />
	</div>

	{#if gameOver}
		<h1>Game Over</h1>
	{/if}
</div>
