<script>
import { userDetails } from "../stores/user.js";
import { goto } from "$app/navigation";

const checkingData = $userDetails;
console.log("Checking Data -> ", checkingData)


// contains  the passcode to be verified
let passcode = [];
var email = "";
var current_email = "yo";
var otp_recieved = 1;
let wrong_otp = false;


// function to generate OTP
async function generateOtp(){
    if(!!email) {
     const url = "http://192.168.1.10:5000/verify?email=" + email; 
     console.log(url);
     const otp_resp = await fetch(url).then(response => response.json()).then(data => otp_recieved = data.toString());
     console.log("otp_recieved -> ", otp_recieved);
    } else {
        // Throw Error if email empty
        console.log("email cannot be empty")
    }
    };

function verifyTheOtp() {
    var inputOtp = "";
    for(var i=0; i <passcode.length; i++) {
        inputOtp += passcode[i];
    }
    if(otp_recieved === inputOtp) {
        console.log("Otp verification Successful")
        $userDetails = {
            "email": email,
            "loggedin": true,
        }
        console.log(JSON.stringify($userDetails));
        var user_route = "/user/" + email;
        goto(user_route);
    } else {
        // prompt wrong OTP here
        console.log("OTP verify fail")
        wrong_otp = true;
    }
}


let background_url = 'https://acegif.com/wp-content/uploads/halloween-gif-animated-81.gif';

$: if(wrong_otp === true) {
    background_url = "https://media.giphy.com/avatars/christianwhite/eLlCBMGqniDh.gif";
}

</script>

<svelte:head>
    <title>Treat and Regards</title>
</svelte:head>


<style>
input[type=number] {
    background-color: black;
    color: white;
    font-weight: bolder;
    height: 20vh;
    font-size: xxx-large ;
    align-items: center;
    align-content: center;
    text-align: center;
    background-image: url('https://images.emojiterra.com/google/android-10/512px/1f383.png') ;
    background-size: 25vh 25vh;
    filter: invert(0.3)
}
/* input[type="number"]:focus {
    
} */

.text-box-div {
    margin-left: auto;
}

.email {
    text-align: center;
}
input[type=email] {
    background-color: slateblue;
    color: white;
    height: 5vh;
    margin-left: 20em;
    margin-right: 20em;
}
button {
    margin-top: 10px;
    background-color: red;
    color: aliceblue;
    height: auto;
}
main {
    background-color: black;
    height: 100%;
    width: 100%;
    margin: 0;
    /* bottom: 0; */
    position: fixed;
    background-image: url('https://acegif.com/wp-content/uploads/halloween-gif-animated-81.gif');
    /* background-image: url(${background_url}); */
    background-repeat: no-repeat;
    background-size: cover;
}

</style>

{#if wrong_otp === false}

<main style="background-image: ${background_url};">
<!-- {passcode}
{email} -->


<div class="flex flex-col align-middle justify-center text-center">
    <h1 style="color: white;" class="text-xl">Enter Your Email</h1>
    <input type="email" class="email" bind:value={email}/>
    <button on:click="{generateOtp}">Generate OTP</button>
</div>

{otp_recieved}

{#if otp_recieved != 1}

<div class="flex flex-col align-middle align-middle justify-center text-center">
    Enter Your 6 digit OTP
</div>
<div class="flex flex-col align-middle justify-center text-box-div">
<div class="py-2 grid gap-2 grid-cols-6 md:grid-cols-6 align-middle justify-center text-center">
    <span class="flex flex-col" >
        <input type="number" id="id1" bind:value="{passcode[0]}"/>
    </span>
    <span class="flex flex-col" >
        <input type="number"  id="id2" bind:value="{passcode[1]}"/>
    </span>
    <span class="flex flex-col" >
        <input type="number"  id="id3"  bind:value="{passcode[2]}" />
    </span>
    <span class="flex flex-col" >
        <input type="number" id="id4" bind:value="{passcode[3]}"/>
    </span>
    <span class="flex flex-col" >
        <input type="number"  id="id5" bind:value="{passcode[4]}"/>
    </span>
    <span class="flex flex-col" >
        <input type="number"  id="id6" bind:value="{passcode[5]}"/>
    </span>
</div> <br />
<span class="flex flex-col text-center align-middle justify-center">
    <input type="button" on:click="{verifyTheOtp}" name="Verify" value="Verify" class="align-middle justify-center text-center w-1/2 md:w-1/2" style="margin-left:auto;margin-right:auto" />
</span>
</div>
{/if}



</main>
{/if}


{#if wrong_otp === true}
<!-- svelte-ignore a11y-missing-attribute -->
<div class="text-xl text-center">
<img src= "https://media.giphy.com/avatars/christianwhite/eLlCBMGqniDh.gif" style="height:50vh; width:30%; margin-left: 35%; margin-right: 35%;" >
<span >Give Wrong OTP and the candy Monster will devour all your candies</span>
</div>
{/if}

<!-- style="margin-left: 30%;" -->