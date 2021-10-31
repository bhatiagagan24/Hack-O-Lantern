<script>
    export let candies;
    console.log("candy length", candies.length);

    import Thankyouform from "./thankyouform.svelte";

    var show_popup = false;

    let show_regard_flag = 1;

    if(candies[2] === "Add first Candy Name") {
        show_regard_flag = 0;
    }

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
<!-- {#if show_regard_flag === 1} -->
<button style="color:aliceblue; background-color: black;" on:click={() => {show_popup = show_popup ^ true;}}>Send Regards </button><br>
<!-- {/if} -->
</div>


{#if show_popup == true}
<Thankyouform></Thankyouform>
{/if}

</main>