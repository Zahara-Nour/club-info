<script>
	import '@skeletonlabs/skeleton/themes/theme-skeleton.css'
	import '@skeletonlabs/skeleton/styles/all.css'
	import '../app.postcss'
	import { AppShell, AppBar } from '@skeletonlabs/skeleton'
	import { LightSwitch } from '@skeletonlabs/skeleton'
	import logo from '$lib/images/logo-petit.png'
</script>

<!-- App Shell -->
<AppShell slotSidebarLeft="bg-surface-500/5 w-56 p-4">
	<svelte:fragment slot="header">
		<!-- App Bar -->
		<AppBar>
			<svelte:fragment slot="lead">
				<img alt="logo" src={logo} class="pr-4 h-12" />
				<strong class="text-xl uppercase">Les Geeks</strong>
			</svelte:fragment>
			<svelte:fragment slot="trail">
				<a
					class="btn btn-sm variant-ghost-surface"
					href="https://discord.gg/EXqV7W8MtY"
					target="_blank"
					rel="noreferrer">Discord</a
				>
				<LightSwitch />
			</svelte:fragment>
		</AppBar>
	</svelte:fragment>
	<!-- Page Route Content -->
	<slot />
</AppShell>
