<script lang="ts">
	import * as Resizable from '$lib/components/ui/resizable/index.js';
</script>

<Resizable.PaneGroup class="h-screen w-screen" direction="horizontal">
	<Resizable.Pane class="h-full w-full">One</Resizable.Pane>
	<Resizable.Handle />
	<Resizable.Pane class="h-full w-full">Output will be here</Resizable.Pane>
</Resizable.PaneGroup>
