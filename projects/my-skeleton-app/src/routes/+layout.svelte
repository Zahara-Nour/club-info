<script>
	import '@skeletonlabs/skeleton/themes/theme-skeleton.css'
	import '@skeletonlabs/skeleton/styles/all.css'
	import '../app.postcss'

	import { AppShell, AppBar } from '@skeletonlabs/skeleton'
	import { LightSwitch } from '@skeletonlabs/skeleton'
	import logo from '$lib/images/logo-petit.png'
	import { Toast } from '@skeletonlabs/skeleton'
</script>

<!-- App Shell -->
<AppShell slotSidebarLeft="bg-surface-500/5 w-56 p-4">
	<svelte:fragment slot="header">
		<!-- App Bar -->
		<AppBar>
			<svelte:fragment slot="lead">
				<a href="/" rel="noreferrer">
					<img alt="logo" src={logo} class="h-12" />
				</a>
				<strong class="ml-4 text-xl uppercase">Les Geeks</strong>
				<a class="ml-4 btn btn-sm variant-ghost-surface" href="presentation" rel="noreferrer"
					>Presentation</a
				>
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
	<Toast />
</AppShell>
