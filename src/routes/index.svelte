<script context="module" lang="ts">
	export const prerender = true;
</script>

<script>
	import Panel from "/src/routes/panel/index.svelte"
	import Navigation from "$lib/Navbar/index.svelte"
</script>

<svelte:head>
	<title>Discord login</title>
</svelte:head>
<Navigation/>
<div class="mt-6">
	<Panel/>
</div>