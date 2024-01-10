<script lang="ts">
	import { AppBar } from '@skeletonlabs/skeleton'
	import { LightSwitch } from '@skeletonlabs/skeleton'
	import Burger from './Burger.svelte'

	export let drawerOpen: () => void
</script>

<AppBar class="shadow-2xl">
	<svelte:fragment slot="lead">
		<div class="inline-block">
			<a href="/">
				<strong
					class="text-primary-500 mr-6 inline-block text-xl uppercase"
					style="font-family: 'Baloo 2', sans-serif;">Mon site</strong
				>
			</a>
		</div>
	</svelte:fragment>
	<svelte:fragment slot="trail">
		<LightSwitch />

		<Burger class=" btn btn-sm mr-4 lg:hidden" handleClick={drawerOpen} />
	</svelte:fragment>
</AppBar>
