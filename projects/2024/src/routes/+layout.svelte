<script lang="ts">
	import {
		AppShell,
		Drawer,
		Modal,
		Toast,
		getDrawerStore,
		initializeStores,
		storePopup
	} from '@skeletonlabs/skeleton'

	import '../app.pcss'

	import { computePosition, autoUpdate, offset, shift, flip, arrow } from '@floating-ui/dom'
	import Navigation from '$lib/ui/Navigation.svelte'
	import TopBar from '$lib/ui/TopBar.svelte'

	function openDrawer(): void {
		drawer.open({})
	}

	function closeDrawer(): void {
		drawer.close()
	}

	// modals, popups and drawer initialization
	initializeStores()
	storePopup.set({ computePosition, autoUpdate, offset, shift, flip, arrow })
	const drawer = getDrawerStore()
</script>

<Drawer><Navigation drawerClose={closeDrawer} /></Drawer>

<AppShell slotSidebarLeft="bg-surface-100-800-token" regionPage="relative">
	<svelte:fragment slot="header">
		<TopBar drawerOpen={openDrawer} />
	</svelte:fragment>
	<svelte:fragment slot="sidebarLeft">
		<div id="sidebar-left" class="hidden lg:block lg:w-60">
			<Navigation />
		</div>
	</svelte:fragment>
	<svelte:fragment slot="sidebarRight">
		<div id="sidebar-left" class="hidden lg:block" />
	</svelte:fragment>

	<!-- Router Slot -->

	<slot />
	<!-- ---- / ---- -->
	<svelte:fragment slot="pageFooter" />
</AppShell>
