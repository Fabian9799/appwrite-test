<script context="module" lang="ts">
	export const prerender = true;
</script>

<script>
	import { onMount } from "svelte";
	import {sdk} from "../appwrite"
	let name = "Please log in!"

	onMount(() => {
		let promise = sdk.account.get();

		promise.then(
			function (response) {
				console.log(response); // Success
				name = response.name
			},
			function (error) {
				console.log(error); // Failure
			}
		);
	})


	function loginDiscord() {
		sdk.account.createOAuth2Session(
			"discord",
			"https://appwrite-test.fabian9799.cloud/",
			"https://appwrite-test.fabian9799.cloud/"
		);
	}

</script>

<svelte:head>
	<title>Home</title>
</svelte:head>
<h1 class="mx-10 px-3 py-2">{name}</h1>
<button
	on:click={loginDiscord}
	class="mx-10 border-2 border-blue-600 rounded-lg px-3 py-2 text-blue-400 cursor-pointer hover:bg-blue-600 hover:text-blue-200"
	>Login with Discord</button
>
