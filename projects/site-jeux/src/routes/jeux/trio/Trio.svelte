<script>
	import Tile from './Tile.svelte'
	import IconMult from '$lib/icones/IconMult.svelte'
	import IconPlus from '$lib/icones/IconPlus.svelte'
	import IconMinus from '$lib/icones/IconMinus.svelte'
	import IconQuestion from '../../../lib/icones/IconQuestion.svelte'

	export let size = 6
	let classCorrection =
		'flex justify-center items-center mx-4 my-2 w-20 h-20 variant-filled-surface text-3xl '
	let classWin =
		'flex justify-center items-center mx-4 my-2 w-20 h-20 variant-filled-success text-3xl '
	let classLost =
		'flex justify-center items-center mx-4 my-2 w-20 h-20 variant-filled-error text-3xl '
	let tileClass = `w-max grid grid-cols-6 gap-4 my-6`
	let indexs = []
	let grid = []
	let target
	let result
	let op = '+'
	let win = false

	for (let n = 0; n < size * size; n++) {
		const i = Math.floor(n / size) // la ligne
		const j = n % size // la colonne

		if (j === 0) {
			grid[i] = []
		}
		grid[i][j] = {
			status: '',
			n: Math.floor(Math.random() * 9 + 1),
		}
	}
	let selecteds = []

	choseTarget()

	function showSolution() {
		win = true
		for (let i = 0; i < size; i++) {
			for (let j = 0; j < size; j++) {
				grid[i][j].status = 'not_available'
			}
		}
		selecteds = [...target.cells]
		selecteds.forEach((selected) => {
			grid[selected.i][selected.j].status = 'selected'
		})
		op = target.op
	}

	function toggleOp() {
		op = op === '+' ? '-' : '+'
	}

	function handleClick(i, j) {
		result = null
		for (let i = 0; i < size; i++) {
			for (let j = 0; j < size; j++) {
				grid[i][j].status = ''
			}
		}

		// si on clique sur une case déjà sélectionnée
		if (selecteds.some((selected) => selected.j === j && selected.i === i)) {
			selecteds = selecteds.filter((selected) => !(selected.j === j && selected.i === i))
		} else if (selecteds.length < 3) {
			selecteds.push({ i, j })
		}

		if (selecteds.length === 2) {
			const min_i = Math.min(selecteds[0].i, selecteds[1].i)
			const max_i = Math.max(selecteds[0].i, selecteds[1].i)
			const min_j = Math.min(selecteds[0].j, selecteds[1].j)
			const max_j = Math.max(selecteds[0].j, selecteds[1].j)

			for (let i = 0; i < size; i++) {
				for (let j = 0; j < size; j++) {
					if (
						!(
							// il y a un trou
							(
								(min_j < j && j < max_j && min_i < i && i < max_i) ||
								(min_j === max_j && j === min_j && min_i < i && i < max_i) ||
								(min_i === max_i && i === min_i && min_j < j && j < max_j) ||
								// pas de trou
								// les éléments se suivent sous la même progression

								(max_j - min_j <= 1 &&
									max_i - min_i <= 1 &&
									((selecteds[0].j - j === selecteds[1].j - selecteds[0].j &&
										selecteds[0].i - i === selecteds[1].i - selecteds[0].i) ||
										(j - selecteds[1].j === selecteds[1].j - selecteds[0].j &&
											i - selecteds[1].i === selecteds[1].i - selecteds[0].i)))
							)
						)
					) {
						grid[i][j].status = 'not_available'
					}
				}
			}
		} else if (selecteds.length === 1) {
			const selected = selecteds[0]
			for (let i = 0; i < size; i++) {
				for (let j = 0; j < size; j++) {
					if (
						!(
							Math.abs(selected.i - i) <= 2 &&
							Math.abs(selected.j - j) <= 2 &&
							(selected.j === j ||
								selected.i === i ||
								Math.abs(selected.j - j) === Math.abs(selected.i - i))
						)
					) {
						grid[i][j].status = 'not_available'
					}
				}
			}
		} else if (selecteds.length === 3) {
			for (let i = 0; i < size; i++) {
				for (let j = 0; j < size; j++) {
					grid[i][j].status = 'not_available'
				}
			}
			const number1 = parseInt(grid[selecteds[0].i][selecteds[0].j].n, 10)
			const number2 = parseInt(grid[selecteds[1].i][selecteds[1].j].n, 10)
			const number3 = parseInt(grid[selecteds[2].i][selecteds[2].j].n, 10)
			result = op === '+' ? number1 * number2 + number3 : number1 * number2 - number3
		}

		selecteds.forEach((selected) => {
			grid[selected.i][selected.j].status = 'selected'
		})

		if (result && result === target.value) {
			win = true
		}
	}

	function choseTarget() {
		win = false

		do {
			target = {}
			target.cells = []
			target.op = Math.random() < 0.5 ? '+' : '-'
			let i = Math.floor(Math.random() * size)
			let j = Math.floor(Math.random() * size)
			target.cells.push({ i, j })
			let direction
			for (let count = 0; count < 2; count++) {
				const directions = []
				if (i > 0 && j > 0) {
					directions.push('up-left')
				}
				if (i > 0) {
					directions.push('up')
				}
				if (i > 0 && j < size - 1) {
					directions.push('up-right')
				}
				if (j > 0) {
					directions.push('left')
				}
				if (j < size - 1) {
					directions.push('right')
				}
				if (i < size - 1 && j > 0) {
					directions.push('down-left')
				}
				if (i < size - 1) {
					directions.push('down')
				}
				if (i < size - 1 && j < size - 1) {
					directions.push('down-right')
				}
				if (directions.length !== 0) {
					direction = direction || directions[Math.floor(Math.random() * directions.length)]

					//  il faut vérifier que la dernière direction est toujours possible
					if (directions.includes(direction)) {
						switch (direction) {
							case 'up-left':
								i--
								j--
								break
							case 'up':
								i--
								break
							case 'up-right':
								i--
								j++
								break
							case 'left':
								j--
								break
							case 'right':
								j++
								break
							case 'down-left':
								i++
								j--
								break
							case 'down':
								i++
								break
							case 'down-right':
								i++
								j++
								break
						}
						target.cells.push({ i, j })
					}
				}
			}
			if (target.cells.length === 3) {
				const number1 = parseInt(grid[target.cells[0].i][target.cells[0].j].n, 10)
				const number2 = parseInt(grid[target.cells[1].i][target.cells[1].j].n, 10)
				const number3 = parseInt(grid[target.cells[2].i][target.cells[2].j].n, 10)
				target.value = target.op === '+' ? number1 * number2 + number3 : number1 * number2 - number3
				if (isNaN(target.value)) throw new Error('target.value is NaN')
			} else {
				target.value = null
			}
		} while (!target.value || target.value < 0)
	}
</script>

<div class="flex">
	<div class="flex flex-col justify-center mx-12">
		<span class={classCorrection}>
			{#if selecteds.length >= 1}
				{grid[selecteds[0].i][selecteds[0].j].n}
			{:else}
				<IconQuestion />
			{/if}
		</span>
		<span class={classCorrection}>
			<IconMult />
		</span>

		<span class={classCorrection}>
			{#if selecteds.length >= 2}
				{grid[selecteds[1].i][selecteds[1].j].n}
			{:else}
				<IconQuestion />
			{/if}
		</span>
		<span on:keydown={() => {}} on:click={toggleOp} class={classCorrection}>
			{#if op === '+'}
				<IconPlus />
			{:else}
				<IconMinus />
			{/if}
		</span>
		<span class={classCorrection}>
			{#if selecteds.length === 3}
				{grid[selecteds[2].i][selecteds[2].j].n}
			{:else}
				<IconQuestion />
			{/if}
		</span>
		<span class={classCorrection}> = </span>
		<span class={win ? classWin : classLost}>
			{target && target.value}
		</span>
	</div>
	<div class="flex flex-col items-center">
		<div class={tileClass}>
			{#each grid as row, i}
				{#each row as cell, j}
					<Tile n={cell.n} on:click={() => handleClick(i, j)} status={cell.status} />
				{/each}
			{/each}
		</div>
	</div>
	<div lass="flex flex-col justify-center mx-12">
		<button class="btn variant-filled-primary" on:click={choseTarget}>Nouvelle cible</button>
	</div>
	<div lass="flex flex-col justify-center mx-12">
		<button class="btn variant-filled-primary" on:click={showSolution}>Solution</button>
	</div>
</div>
