<script>

let background_gifs = ['https://media.giphy.com/media/mrntmDtLQdILS/giphy.gif', 'https://media.giphy.com/media/17fRLuQyHvv4k/giphy.gif', 'https://media.giphy.com/media/1APcmTq0EMjNYWRuQM/giphy.gif'];


function whichGifNow() {
// generate random number
    const totalGif = background_gifs.length;
    const curGif = Math.floor(Math.random() * totalGif);
    background_url = background_gifs[curGif];
}

$: setInterval(whichGifNow, 7000);

</script>

<style>
    img {
        filter: invert(0.1);
    }
</style>

<div>
    <img src="{background_gifs}" />
</div>