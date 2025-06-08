<script lang="ts">
	import { Button } from '$lib/components/ui/button/index.js';
	import * as Resizable from '$lib/components/ui/resizable/index.js';
	import * as Menubar from '$lib/components/ui/menubar/index.js';
	import Play from 'lucide-svelte/icons/play';
	import Reload from 'lucide-svelte/icons/refresh-cw';
	import Monaco from 'svelte-monaco';
	import { onMount } from 'svelte';

	let direction = <'horizontal' | 'vertical'>$state('horizontal');
	let autoRun = $state(false);
	let code = $state(`<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

</body>
</html>`);

	function run() {
		const outputframe = document.getElementById('output') as HTMLIFrameElement;
		if (outputframe) {
			outputframe.srcdoc = code;
		}
	}

	$effect(() => {
		if (autoRun) {
			const outputframe = document.getElementById('output') as HTMLIFrameElement;
			if (outputframe) {
				outputframe.srcdoc = code;
			}
		}
	});
</script>

<Resizable.PaneGroup class="h-screen w-screen" {direction}>
	<Resizable.Pane class="h-full w-full">
		<div class="flex h-full w-full flex-col gap-3 p-3">
			<Menubar.Root class="h-fit">
				<Menubar.Menu>
					<Menubar.Trigger>File</Menubar.Trigger>
					<Menubar.Content>
						<Menubar.Item>Save</Menubar.Item>
						<Menubar.Item>Open</Menubar.Item>
					</Menubar.Content>
				</Menubar.Menu>
				<Menubar.Menu>
					<Menubar.Trigger>Settings</Menubar.Trigger>
					<Menubar.Content>
						<Menubar.Item
							onclick={() => (direction = direction === 'horizontal' ? 'vertical' : 'horizontal')}
						>
							Switch to {direction === 'horizontal' ? 'vertical' : 'horizontal'} split
						</Menubar.Item>
						<Menubar.Item onclick={() => (autoRun = !autoRun)}>
							{autoRun ? 'Disable' : 'Enable'} autorun
						</Menubar.Item>
					</Menubar.Content>
				</Menubar.Menu>
				<div class="grow"></div>
				<Button variant="ghost" size="icon" onclick={run}>
					<Play />
				</Button>
			</Menubar.Root>
			<div class="h-full w-full overflow-hidden rounded-lg">
				<Monaco
					options={{ language: 'html', automaticLayout: true }}
					theme="vs-dark"
					on:ready={(event) => console.log(event.detail)}
					bind:value={code}
				/>
			</div>
		</div>
	</Resizable.Pane>
	<Resizable.Handle />
	<Resizable.Pane class="h-full w-full">
		<iframe title="Output" class="h-full w-full" id="output" frameborder="0"></iframe>
	</Resizable.Pane>
</Resizable.PaneGroup>
