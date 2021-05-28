<script>
	import { page } from "$app/stores";
	import { onMount } from "svelte";

	let slug = $page.params.id;
	let status = 0;
	let data;
	let question;
	import { sdk } from "../../appwrite";
	onMount(() => {
		let promise = sdk.database.getDocument("60a4524fa1134", slug);

		promise.then(
			function (response) {
				data = response;
				status = 1;
				question = data.question;
			},
			function (error) {
				status = 2;
			}
		);
	});
</script>

<svelte:head>
	<title>{question}</title>
</svelte:head>

<div class="hero bg-base-200 text-white rounded-lg">
	{#if status == 1}
		<div class="text-center hero-content mb-5 mt-5">
			<div class="max-w-md">
				<h1 class="mb-5 text-5xl font-bold">{question}</h1>
				{#each data.answers as item}
					<div class="btn btn-primary w-80 mt-5">
						{item}
					</div>
				{/each}
				<div class="btn btn-secondary w-80 mt-5">
					Answer: {data.result}
				</div>
				{#if !data}
					<div class="btn btn-primary w-80 mt-5">Loading...</div>
				{/if}
			</div>
		</div>
	{/if}
	{#if status == 2}
		<div class="text-center hero-content mb-5 mt-5">
			<div class="max-w-md">
				<h1 class="mb-5 text-5xl font-bold">Unknown Poll</h1>
			</div>
		</div>
	{/if}
</div>

