<script>
    export let question = "No question provided"
    export let id
    let buttonText = "DELETE"
    let status = false
    let css = "bg-red-500"
    import { sdk } from "../../appwrite";
    function deleteEntry() {
        let promise = sdk.database.deleteDocument('60a4524fa1134', id);

promise.then(function (response) {
    console.log(response); // Success
    status = true
    css = "cursor-not-allowed bg-green-500"
    buttonText = "Deleted!"
}, function (error) {
    console.log(error); // Failure
    alert("Dude you don't have permission")
});
    }
</script>


<div class="p-2 lg:w-1/3 md:w-1/2 w-full">
    <div class="h-full flex items-center border-gray-800 border p-4 rounded-lg">
      <div class="flex-grow">
        <h2 class="text-white title-font font-medium">{question}</h2>
          <button on:click={deleteEntry} class="{css} inline-flex mt-4 text-white border-0 py-2 px-6 focus:outline-none w-full rounded text-lg" disabled={status}>{buttonText}</button>
      </div>
    </div>
  </div>