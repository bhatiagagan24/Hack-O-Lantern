<script>
    export let candies;
    console.log(candies);


</script>

<style>
    /* .yo {
        margin-left: 200px;
    } */
</style>




<div class="text-center align-middle border-2 py-5">
{#each candies as candy}
<em><strong>
{candy}
</strong>
</em>
<br>
{/each}
<br>
<button>Delete</button> <br>
<button>Send Regards </button><br>
<button>Add more Recepients</button>
</div>

