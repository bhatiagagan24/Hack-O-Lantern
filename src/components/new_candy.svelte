<script>
    let given_by = '';
    let candy_name = '';
    let flavour = '';
    export let user;
</script>



<div class="align-middle justify-center text-center py-10">
    <button style="color:white; background-color:black; width:10em" class="rounded-md hover:shadow-md">New Candy</button>
</div>

<!-- 
let given_by = "";
let candy_name = "";
let flavour = ""; -->

<form>
    <input type="text" bind:value={given_by} />
    <input type="text" bind:value={candy_name} />
    <input type="text" bind:value={flavour} />
    <button on:click={() => {
        user["userdata"].push({
            "flavour": flavour,
            "name": candy_name,
            "givenby": given_by,

        });
        user = user;
    }}> Submit</button>
</form>