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
        if(response.teams[0].name == "Admin"){
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
  <section class="text-gray-400 bg-gray-900 body-font">
    <div class="container px-5 py-4 pt-20 mx-auto">
      <div class="flex flex-col text-center w-full">
        <h1 class="sm:text-3xl text-2xl font-medium title-font mb-4 text-white">
          Edit documents!
        </h1>
      </div>
      <div class="flex flex-wrap">
        {#each data.documents as data, i}
          <Card question={data.question} id={data.$id} />
        {/each}
      </div>
    </div>
  </section>
  <Create/>
{:else}
  <section class="text-gray-400 bg-gray-900 body-font">
    <div class="container px-5 py-4 mx-auto">
      <div class="flex flex-col text-center w-full mb-20">
        <h1 class="sm:text-3xl text-2xl font-medium title-font mb-4 text-white">
          You don't have access to the panel!
        </h1>
      </div>
    </div>
  </section>{/if}
