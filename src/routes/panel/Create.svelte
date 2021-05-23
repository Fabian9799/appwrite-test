<script>
    import { sdk } from "../../appwrite";
    let question;
    let options;
    let answer;
    function createPoll() {
        options = options.split(",");
        let data = {
            question: question,
            answers: options,
            result: answer,
        };
        let promise = sdk.database.createDocument(
            "60a4524fa1134",
            data,
            ["*"],
            ["team:60a64fce28ddd"]
        );

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

<section class="text-gray-400 bg-gray-900 body-font relative">
    <div class="container px-5 py-4 mx-auto flex sm:flex-nowrap flex-wrap">
        <div class="flex flex-col md:ml-auto w-full md:py-8 md:mt-0">
            <h2 class="text-white text-lg mb-1 font-medium title-font">
                Create Poll
            </h2>
            <div class="relative mb-4">
                <label for="question" class="leading-7 text-sm text-gray-400"
                    >Question</label
                >
                <input
                    bind:value={question}
                    type="text"
                    id="question"
                    name="question"
                    class="w-full bg-gray-800 rounded border border-gray-700 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-900 text-base outline-none text-gray-100 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
                />
            </div>
            <div class="relative mb-4">
                <label for="options" class="leading-7 text-sm text-gray-400"
                    >Options (add multiple by adding a comma</label
                >
                <input
                    bind:value={options}
                    type="text"
                    id="options"
                    name="options"
                    class="w-full bg-gray-800 rounded border border-gray-700 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-900 text-base outline-none text-gray-100 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
                />
            </div>
            <div class="relative mb-4">
                <label for="answer" class="leading-7 text-sm text-gray-400"
                    >Answer</label
                >
                <input
                    bind:value={answer}
                    type="text"
                    id="answer"
                    name="answer"
                    class="w-full bg-gray-800 rounded border border-gray-700 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-900 text-base outline-none text-gray-100 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
                />
            </div>

            <button
                on:click={createPoll}
                class="text-white bg-indigo-500 border-0 py-2 px-6 focus:outline-none hover:bg-indigo-600 rounded text-lg"
                >Send</button
            >
        </div>
    </div>
</section>
