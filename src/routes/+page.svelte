<script lang="ts">
	import { Button } from '$lib/components/ui/button/index.js';
	import * as Resizable from '$lib/components/ui/resizable/index.js';
	import * as Menubar from '$lib/components/ui/menubar/index.js';
	import Play from 'lucide-svelte/icons/play';
	import Reload from 'lucide-svelte/icons/refresh-cw';
	import { mode, toggleMode } from 'mode-watcher';

	let direction = <'horizontal' | 'vertical'>$state('horizontal');
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
					<Menubar.Trigger>View</Menubar.Trigger>
					<Menubar.Content>
						<Menubar.Item
							onclick={() => (direction = direction === 'horizontal' ? 'vertical' : 'horizontal')}
						>
							Switch to {direction === 'horizontal' ? 'vertical' : 'horizontal'} split
						</Menubar.Item>
						<Menubar.Item onclick={toggleMode}>
							Switch to {$mode === 'light' ? 'dark' : 'light'} mode
						</Menubar.Item>
					</Menubar.Content>
				</Menubar.Menu>
				<div class="grow"></div>
				<Button variant="ghost" size="icon">
					<Reload />
				</Button>
				<Button variant="ghost" size="icon">
					<Play />
				</Button>
			</Menubar.Root>
			<div id="monaco" class="h-full w-full rounded"></div>
		</div>
	</Resizable.Pane>
	<Resizable.Handle />
	<Resizable.Pane class="h-full w-full">Output will be here</Resizable.Pane>
</Resizable.PaneGroup>
