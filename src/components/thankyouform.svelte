


<script>
    // Make API request to send email to these people

    async function sendThanks() {
        const form_resp = await fetch("http://192.168.1.10:5000/test").then(response => response.json()).then(data => console.log(data))
    }

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


<main>
    <div class="text-center py-8">
        <form on:submit={sendThanks}>
            <input type="textbox" placeholder="Email"/> <br> <br>
            <textarea placeholder="Message"/> <br><br>
            <input type="submit" name="submit"/>
        </form>
    </div>
</main>