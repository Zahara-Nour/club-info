<script lang="ts">
	import { AppBar, Avatar, modeCurrent, modeOsPrefers, popup } from '@skeletonlabs/skeleton';
	import { LightSwitch } from '@skeletonlabs/skeleton';
	import { get } from 'svelte/store';
	import Burger from './Burger.svelte';

	export let drawerOpen: () => void;
	const avatar = '/images/avatars/avatar-teacher-boy.jpg';
</script>

<AppBar class="shadow-2xl">
	<svelte:fragment slot="lead">
		<div class="inline-block">
			<a href="/">
				<strong
					class="lg:text-primary-500 hidden lg:mr-6 lg:inline-block lg:text-xl lg:uppercase"
					style="font-family: 'Baloo 2', sans-serif;">Ubumaths</strong
				>
			</a>
		</div>
	</svelte:fragment>
	<svelte:fragment slot="trail">
		<LightSwitch />

		<Burger class=" btn btn-sm mr-4 lg:hidden" handleClick={drawerOpen} />
	</svelte:fragment>
</AppBar>
