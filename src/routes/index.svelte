<script context="module" lang="ts">
	export const prerender = true;
</script>

<script>
	import { onMount } from "svelte";
	import { sdk } from "../appwrite";
	import ThemeSwitcher from "$lib/ThemeSwitcher/index.svelte"
	let user;
	let name = "";
	let image =
		"https://discord.com/assets/6debd47ed13483642cf09e832ed0bc1b.png";
	onMount(() => {
		let promise = sdk.account.get();

		promise.then(
			function (response) {
				user = response;
				name = user.name;

				let promise = sdk.account.getSessions();

				promise.then(
					function (response) {
						fetch("https://discord.com/api/users/@me", {
							headers: {
								authorization: `Bearer ${response.sessions[0].providerToken}`,
							},
						})
							.then((result) => result.json())
							.then((response) => {
								image = `https://cdn.discordapp.com/avatars/${response.id}/${response.avatar}.webp?size=128`;
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
<div class="navbar mb-2 shadow-lg bg-neutral text-neutral-content rounded-box">
	<div class="flex-none px-2 mx-2">
		<span class="text-lg font-bold"> SomeTitle </span>
	</div>
	<div class="flex-1 px-2 mx-2">
		{#if user}
			<div class="items-stretch lg:flex">
				<a href="/panel" class="btn btn-ghost btn-sm rounded-btn">
					Panel
				</a>
			</div>
			<div class="items-stretch lg:flex">
				<a
					on:click={logoutDiscord}
					class="btn btn-ghost btn-sm rounded-btn"
				>
					Logout
				</a>
			</div>
		{:else}
			<div class="items-stretch hidden lg:flex">
				<a
					on:click={loginDiscord}
					class="btn btn-ghost btn-sm rounded-btn"
				>
					Login
				</a>
			</div>
		{/if}
	</div>
	<div class="flex-none hidden px-2 mx-2 lg:flex">
		<div class="flex items-stretch">
			<ThemeSwitcher/>
		</div>
	</div>
	<div class="flex-none">
		<div class="flex items-stretch">
			{#if user}
			<button class="btn no-animation">{name}</button>
			{/if}
		</div>
		<div class="flex-none">
			<div class="avatar">
				<div class="rounded-full w-10 h-10 m-1">
					<img src={image} />
				</div>
			</div>
		</div>
	</div>
</div>