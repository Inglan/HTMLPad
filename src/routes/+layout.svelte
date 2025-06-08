<script lang="ts">
	import '../app.css';
	import { ModeWatcher } from 'mode-watcher';
	let { children } = $props();
</script>

<svelte:head>
	<title>HTMLPad</title>
</svelte:head>

<ModeWatcher defaultMode="dark" />
{@render children()}
