<script>
    let data;
    import { Appwrite } from "appwrite";
    let sdk = new Appwrite();

    sdk.setEndpoint("https://api.fa97.de/v1") // Your API Endpoint
        .setProject("60a2e6bf46842"); // Your project ID

    let promise = sdk.database.listDocuments("60a4524fa1134");

    promise.then(
        function (response) {
            console.log(response);
            data = response.documents;
        },
        function (error) {
            console.log(error); // Failure
        }
    );
</script>

<section class="bg-white">
    <div class="flex flex-wrap overflow-hidden">
        <div class="w-full overflow-hidden md:w-1/3 lg:w-1/3 xl:w-1/3">
            <!-- Column Content -->
        </div>

        <div class="shadow-2xl w-full overflow-hidden md:w-1/3 lg:w-1/3 xl:w-1/3 m-20 bg-gradient-to-r from-blue-500 to-blue-700 rounded-md">
            <div class="shadow-md rounded-md overflow-hidden text-center">
                <div class="text-white m-5 text-5xl font-semibold">
                    Questions
                </div>

                {#if data}
                    {#each data as item}
                        <a href="/poll/{item.$id}" class="no-underline">
                            <div
                                class="shadow-2xl m-5 bg-white text-blue-500 px-6 py-3 mt-4 rounded-md shadow-md text-xl font-semibold uppercase transform duration-200 ease-in-out focus:outline-none hover:-translate-y-1"
                            >
                                {item.question}
                            </div>
                        </a>
                    {/each}
                {/if}
                {#if !data}
                    <div
                        class="m-5 bg-white text-blue-500 px-6 py-3 mt-4 rounded-md shadow-md text-xl font-semibold uppercase transform duration-200 ease-in-out focus:outline-none hover:-translate-y-1"
                    >
                        Loading
                    </div>
                {/if}
            </div>
        </div>

        <div class="w-full overflow-hidden md:w-1/3 lg:w-1/3 xl:w-1/3">
            <!-- Column Content -->
        </div>
    </div>
</section>
