<script>
    export let question = "No question provided"
    export let id
    export let answers = "No answer provided"
    export let result = "No result provided"
    let buttonText = "DELETE"
    let status = false
    let css = "btn btn-primary"
    import { sdk } from "../../appwrite";
    function deleteEntry() {
        let promise = sdk.database.deleteDocument('60a4524fa1134', id);

promise.then(function (response) {
    console.log(response); // Success
    status = true
    css = "cursor-not-allowed btn btn-secondary"
    buttonText = "Deleted!"
}, function (error) {
    console.log(error); // Failure
    alert("Dude you don't have permission")
});
    }
</script>

<div class="card flex-grow m-5 lg:w-1/3 md:w-1/3 w-full shadow-lg bg-base-200">
  <div class="card-body">
    <h2 class="card-title">{question}</h2> 
    <p>Answers: {answers}</p> 
    <p>Result: {result}</p> 
    <div class="card-actions">
      <button on:click={deleteEntry} class={css}>Delete</button> 
    </div>
  </div>
</div> 