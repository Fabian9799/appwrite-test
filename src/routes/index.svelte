<script context="module" lang="ts">
	export const prerender = true;
</script>

<script>
	import { Appwrite } from "appwrite";
	import { onMount } from "svelte";
	let sdk = new Appwrite();

	sdk.setEndpoint("https://api.fa97.de/v1") // Your API Endpoint
		.setProject("60a2e6bf46842"); // Your project ID

	onMount(() => {
		let promise = sdk.account.get();

		promise.then(
			function (response) {
				console.log(response); // Success
			},
			function (error) {
				console.log(error); // Failure
			}
		);
	})


	function loginDiscord() {
		sdk.account.createOAuth2Session(
			"discord",
			"http://localhost:3000",
			"http://localhost:3000"
		);
	}
</script>

<svelte:head>
	<title>Home</title>
</svelte:head>
<h1>TEST</h1>
<button
	on:click={loginDiscord}
	class="m-10 border-2 border-blue-600 rounded-lg px-3 py-2 text-blue-400 cursor-pointer hover:bg-blue-600 hover:text-blue-200"
	>Login with Discord</button
>
