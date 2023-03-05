<script>
	export let n
	export let status = ''
	const baseClass = 'btn my-1 h-24 w-24 size text-2xl flex items-center justify-center'
</script>

<button
	class={'btn my-1 h-24 w-24 size text-3xl flex items-center justify-center ' +
		(status === 'selected' ? 'variant-filled-tertiary' : 'bg-white text-black')}
	on:click
	disabled={status === 'not_available'}
>
	{n}
</button>

<style lang="postcss">
</style>
