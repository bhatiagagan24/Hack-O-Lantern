


<script>
    // Make API request to send email to these people

    async function sendThanks() {
        console.log("Thanked")
    }

</script>


<style>
    input, textarea {
        background-color: black;
        color: white;
    }
</style>


<main>
    <div class="text-center py-8 ">
        <form on:submit={sendThanks}>
            <input type="textbox" placeholder="Email"/> <br> <br>
            <textarea placeholder="Message"/> <br><br>
            <input type="submit" name="submit"/>
        </form>
    </div>
</main>