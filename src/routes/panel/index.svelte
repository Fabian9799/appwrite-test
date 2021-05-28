<script>
  import { onMount } from "svelte";
  import { sdk } from "../../appwrite";
  import Card from "./Card.svelte";
  import Create from "./Create.svelte";
  let data;
  onMount(() => {
    let promise = sdk.teams.list("60a64fce28ddd");

    promise.then(
      function (response) {
        if (response.teams[0].name == "Admin") {
          let promise = sdk.database.listDocuments("60a4524fa1134");

          promise.then(
            function (response) {
              data = response;
            },
            function (error) {
              console.log(error); // Failure
            }
          );
        }
      },
      function (error) {
        console.log(error); // Failure
      }
    );
  });
</script>

{#if data}
<div class="card lg:card-side bordered text-white">
  <div class="card-body">
    <div class="flex flex-col text-center w-full">
      <h2 class="card-title text-center text-5xl font-bold">Edit documents</h2> 
    </div>
    <div class="flex flex-wrap">
      {#each data.documents as data, i}
        <Card question={data.question} id={data.$id} answers={data.answers} result={data.result}/>
      {/each}
    </div>
  </div>
  
</div>

  <Create />
{:else}
<div class="alert">
  <div class="flex-1 text-neutral-content">
    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="#ff5722" class="w-6 h-6 mx-2"><!----> <!----> <!----> <!----> 
      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M18.364 18.364A9 9 0 005.636 5.636m12.728 12.728A9 9 0 015.636 5.636m12.728 12.728L5.636 5.636"></path> <!----> <!----> <!----> <!----> <!----> <!----> <!----> <!----> <!----> <!----> <!----> <!----> <!----> <!----> <!----> <!----> <!----> <!----> <!----> <!----> <!----> <!---->
    </svg> 
    <label>You don't have access to the panel!</label>
  </div> 
  <div class="flex-none">
  </div>
</div>
{/if}
