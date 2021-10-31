


<script>
    // Make API request to send email to these people

    async function sendThanks() {
        let uri = `http://192.168.1.10:5000/send/email?recemail=${recemail}&message=${message}` 
        const form_resp = await fetch(uri).then(response => response.json()).then(data => {
            if(data == 1) {
                message_sent = true;
            }
        })

    }

    let recemail = '';
    let message = '';

    let message_sent = false;

</script>


<style>
    input, textarea {
        background-color: blanchedalmond;
        color: black;
        padding:10px;
        border: 2px red solid;
        width:30%;
        font-weight: 500;
    }
</style>

{#if message_sent === false}
<main>
    <div class="text-center py-8 ">
            <input type="textbox" placeholder="Email" bind:value="{recemail}" required/> <br> <br>
            <textarea placeholder="Message" bind:value="{message}" required/> <br><br>
            <input type="submit" name="submit" on:click={sendThanks} />
    </div>
</main>
{/if}