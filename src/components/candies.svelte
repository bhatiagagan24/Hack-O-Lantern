<script>
    export let candies;
    console.log("candy length", candies.length);

    import Thankyouform from "./thankyouform.svelte";

    var show_popup = false;

</script>

<style>
    main {
        margin-left: 20px;
        margin-right: 20px;
    }
</style>



<main>
<div class=" text-center align-middle border-2 py-5">
{#each candies as candy, i}
<em><strong>
{candy}
</strong>
</em>
<br>
<br>
{/each}
<button style="color:aliceblue; background-color: black;" on:click={() => {show_popup = show_popup ^ true;}}>Send Regards </button><br>
</div>


{#if show_popup == true}
<Thankyouform></Thankyouform>
{/if}

</main>