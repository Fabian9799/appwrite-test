<script context="module" lang="ts">
	export const prerender = true;
</script>

<script>
	import { onMount } from "svelte";
	import { sdk } from "../appwrite";
	let user;
	let image
	onMount(() => {
		let promise = sdk.account.get();

		promise.then(
			function (response) {
				console.log(response); // Success
				user = response;

				let promise = sdk.account.getSessions();

				promise.then(
					function (response) {
						console.log(response.sessions[0].providerToken); // Success
						fetch("https://discord.com/api/users/@me", {
							headers: {
								authorization: `Bearer ${response.sessions[0].providerToken}`,
							},
						})
							.then((result) => result.json())
							.then((response) => {
								console.log(response)
								image = `https://cdn.discordapp.com/avatars/${response.id}/${response.avatar}.webp?size=128`
							})
							.catch(console.error);
					},
					function (error) {
						console.log(error); // Failure
					}
				);
			},
			function (error) {
				console.log(error); // Failure
			}
		);
	});

	function loginDiscord() {
		sdk.account.createOAuth2Session(
			"discord",
			import.meta.env.VITE_DISCORD_REDIRECT,
			import.meta.env.VITE_DISCORD_REDIRECT,
			["identify"]
		);
	}

	function logoutDiscord() {
		let promise = sdk.account.deleteSessions();

		promise.then(
			function (response) {
				console.log(response); // Success
				window.location.reload();
			},
			function (error) {
				console.log(error); // Failure
			}
		);
	}
</script>

<svelte:head>
	<title>Discord login</title>
</svelte:head>

{#if user}
<img class="mx-10 px-3 py-2" src={image} alt="">
<h1 class="mx-10 px-3 py-2">{user.name}</h1>
	<a href="/panel">
		<button
			class="mx-10 border-2 border-blue-600 rounded-lg px-3 py-2 text-blue-400 cursor-pointer hover:bg-blue-600 hover:text-blue-200"
			>Access Panel</button
		></a
	>
	<button
		on:click={logoutDiscord}
		class="mx-10 border-2 border-red-600 rounded-lg px-3 py-2 text-red-400 cursor-pointer hover:bg-red-600 hover:text-red-200"
		>Logout</button
	>
{:else}
	<h1 class="mx-10 px-3 py-2">Please Log in!</h1>
	<button
		on:click={loginDiscord}
		class="mx-10 border-2 border-blue-600 rounded-lg px-3 py-2 text-blue-400 cursor-pointer hover:bg-blue-600 hover:text-blue-200"
		>Login with Discord</button
	>
{/if}
