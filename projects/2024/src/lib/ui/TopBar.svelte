<script lang="ts">
	import { AppBar, Avatar, modeCurrent, modeOsPrefers, popup } from '@skeletonlabs/skeleton';
	import { LightSwitch } from '@skeletonlabs/skeleton';
	import Burger from './Burger.svelte';

	export let drawerOpen: () => void;
</script>

<AppBar class="shadow-2xl">
	<svelte:fragment slot="lead">
		<a href="/"><img src="/images/gidouille.png" alt="gidouille" class="mr-4 w-8" /></a>

		<div class="inline-block">
			<a href="/">
				<strong
					class="hidden lg:mr-6 lg:inline-block lg:text-xl lg:uppercase lg:text-primary-500"
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
