<script>
	import { page } from "$app/stores";
	let slug = $page.params.id;
	let status = 0
	let data;
	let question
	import { Appwrite } from "appwrite";
	let sdk = new Appwrite();

	sdk.setEndpoint("https://api.fa97.de/v1") // Your API Endpoint
		.setProject("60a2e6bf46842"); // Your project ID

	let promise = sdk.database.getDocument("60a4524fa1134", slug);

	promise.then(
		function (response) {
			data = response;
			status = 1;
			question = data.question
		},
		function (error) { status = 2}
	);
</script>
<svelte:head>
	<title>{question}</title>
</svelte:head>
<section class="bg-white">
	{#if status == 1}
		<div class="flex flex-wrap overflow-hidden">
			<div class="w-full overflow-hidden md:w-1/3 lg:w-1/3 xl:w-1/3">
				<!-- Column Content -->
			</div>

			<div class="w-full overflow-hidden md:w-1/3 lg:w-1/3 xl:w-1/3 m-20 bg-gradient-to-r from-blue-500 to-blue-700 shadow-2xl rounded-md">
				<div class="shadow-md rounded-md overflow-hidden text-center">
					<div class="text-white m-5 text-5xl font-semibold">
						{data.question}
					</div>
					{#each data.answers as item}
						<div class="p-5">
							<p
								class="text-white text-xl font-semibold uppercase"
							>
								{item}
							</p>
						</div>
					{/each}

					<button
						class="shadow-2xl cursor-default m-5 bg-white text-blue-500 px-6 py-3 mt-4 rounded-md shadow-md text-xl font-semibold uppercase focus:outline-none"
					>
						Answer: {data.result}
					</button>
				</div>
			</div>

			<div class="w-full overflow-hidden md:w-1/3 lg:w-1/3 xl:w-1/3">
				<!-- Column Content -->
			</div>
		</div>
	{/if}
	{#if status == 2}
	<div class="flex flex-wrap overflow-hidden">
		<div class="w-1/3 overflow-hidden">
			<!-- Column Content -->
		</div>

		<div class="w-1/3 overflow-hidden m-20 bg-gradient-to-r from-red-500 to-red-700 shadow-2xl rounded-md">
			<div class="shadow-md rounded-md overflow-hidden text-center">
				<div class="text-white m-5 text-6xl font-semibold">
				Unknown Poll
				</div>


				
			</div>
		</div>

		<div class="w-1/3 overflow-hidden">
			<!-- Column Content -->
		</div>
	</div>
	{/if}
</section>
