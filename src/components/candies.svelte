<script>
    export let candies;
    console.log("candy length", candies.length);

    import Thankyouform from "./thankyouform.svelte";

    var show_popup = false;

    let show_regard_flag = 1;

    if(candies[2] === "Add first Candy Name") {
        show_regard_flag = 0;
    }

    const gifs = ["https://media.giphy.com/media/t2uEYBdHWXEkqx9M9n/giphy.gif", "https://media.giphy.com/media/QuxqWk7m9ffxyfoa0a/giphy.gif", "https://media.giphy.com/media/h2CfczI1ggcspHZ26z/giphy.gif","https://media.giphy.com/media/h8OX1iXpgYoH1wIkHE/giphy.gif"];
    const totalGif = gifs.length;
    const curGif = 3;
</script>

<style>
    main {
        margin-left: 20px;
        margin-right: 20px;
    }
</style>



<main>
<div class="w-64 bg-gray-300	text-center align-middle border-4 p-5 m-5">
{#each candies as candy, i}
        <p class="text-xl text-red-500 font-bold">
            {candy}
        </p>
<br>
{/each}
<!-- {#if show_regard_flag === 1} -->
<img src={gifs[curGif]} alt="fear" />
<button class="bg-transparent hover:bg-red-500 text-red-600 font-semibold hover:text-white py-2 m-5 px-4 border border-red-500 hover:border-transparent rounded" on:click={() => {show_popup = show_popup ^ true;}}>Send Regards </button><br>
<!-- {/if} -->
</div>


{#if show_popup == true}
<Thankyouform></Thankyouform>
{/if}

</main>