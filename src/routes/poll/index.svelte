<script>
    let data;
    import { onMount } from "svelte";
    import { sdk } from "../../appwrite";

    onMount(() => {
        let promise = sdk.database.listDocuments("60a4524fa1134");

        promise.then(
            function (response) {
                console.log(response);
                // @ts-ignore
                data = response.documents;
            },
            function (error) {
                console.log(error); // Failure
            }
        );
    });
</script>

<div class="hero bg-base-200 text-white rounded-lg">
    <div class="text-center hero-content mb-5">
        <div class="max-w-md">
            <h1 class="mb-5 text-5xl font-bold">Polls</h1>
            <p class="mb-5" />
            {#if data}
                {#each data as item}
                    <a href="/poll/{item.$id}" class="no-underline">
                        <div
                            class="btn btn-primary w-80 mt-5"
                        >
                            {item.question}
                        </div>
                    </a>
                {/each}
            {/if}
            {#if !data}
            <div
            class="btn btn-primary w-80 mt-5"
        >
            Loading...
        </div>
            {/if}
        </div>
    </div>
</div>
