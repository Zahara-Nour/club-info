<script lang="ts">
	import Navigation from '$lib/ui/Navigation.svelte';
	import TopBar from '$lib/ui/TopBar.svelte';
	import '../app.pcss';
	import {
		AppShell,
		Drawer,
		getDrawerStore,
		initializeStores,
		storePopup
	} from '@skeletonlabs/skeleton';
	import { computePosition, autoUpdate, offset, shift, flip, arrow } from '@floating-ui/dom';

	function openDrawer() {
		drawer.open({});
	}

	function closeDrawer() {
		drawer.close();
	}

	// modals, popups and drawer initialization
	initializeStores();
	storePopup.set({ computePosition, autoUpdate, offset, shift, flip, arrow });
	const drawer = getDrawerStore();
</script>

<Drawer><Navigation drawerClose={closeDrawer} /></Drawer>

<AppShell slotSidebarLeft="bg-surface-500/5 w-56 p-4">
	<svelte:fragment slot="header">
		<TopBar drawerOpen={openDrawer} />
	</svelte:fragment>
	<svelte:fragment slot="sidebarLeft">
		<!-- Insert the list: -->
		<div id="sidebar-left" class="hidden lg:block lg:w-60">
			<Navigation />
		</div>
		<!-- --- -->
	</svelte:fragment>
	<slot />
</AppShell>
