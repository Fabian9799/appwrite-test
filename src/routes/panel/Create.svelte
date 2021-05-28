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

<div class="card lg:card-side bordered text-white mt-5">
    <div class="card-body">
        <div class="flex flex-col text-center w-full">
            <h2 class="card-title text-center text-5xl font-bold mb-8">
                Create Poll
            </h2>
        </div>
        <div class="flex flex-wrap">
            <div class="p-10 card bg-base-200 w-full">
                <div class="form-control">
                    <label class="label">
                        <span class="label-text">Question</span>
                    </label>
                    <input bind:value={question} type="text" class="input" />
                    <label class="label mt-5">
                        <span class="label-text">Options</span>
                    </label>
                    <input bind:value={options} type="text" class="input" />
                    <label class="label mt-5">
                        <span class="label-text">Answer</span>
                    </label>
                    <input bind:value={answer} type="text" class="input" />
                    <button  on:click={createPoll} class="btn btn-primary mt-10">Create</button>
                </div>
            </div>
        </div>
    </div>
</div>

