<script>
import { userDetails } from "../stores/user.js";
const checkingData = $userDetails;
console.log("Checking Data -> ", checkingData)


// contains  the passcode to be verified
let passcode = [];
var email = "";
var current_email = "yo";
var otp_recieved;

// function to generate OTP
function generateOtp(email) {
    if(email === "") {
     // make a request to the API for generating an OTP. That OTP is recieved here and stored inside a variable which will be 
     // further used for verifying the the user.
    }
};

function verifyTheOtp() {
    var inputOtp = "";
    for(var i=0; i <passcode.length; i++) {
        inputOtp += passcode[i];
    }
    if(otp_recieved === inputOtp) {
        // move to next page and also write to the writable userDetails the detail of the user -> 
        // {
            // "loggedin": true,
            // "email": email,
        // }
        // loggedin will be used to verify the signin and email will be used to fetch the data from the API
    } else {
        // prompt wrong OTP here
    }
}


</script>

<svelte:head>
    <title>Treat and Regards</title>
</svelte:head>


<style>
input[type=number] {
    background-color: tomato;
    height: 20vh;
    font-size: xx-large ;
    align-items: center;
    align-content: center;
    text-align: center;
}
.text-box-div {
    margin-left: auto;
}

.email {
    text-align: center;
}
input[type=email] {
    background-color: slateblue;
}
button {
    background-color: black;
    color: aliceblue;
}

</style>
{passcode}
{email}
<div class="flex flex-col align-middle justify-center text-center">
    <h1 class="text-5xl">Candy Treat Calculator</h1>
    <h1>Some Spooky Theme will be Added here to make the Website look good for the theme</h1>
    <br>
</div>

<div class="flex flex-col align-middle justify-center text-center">
    Enter Your Email here
    <input type="email" class="email" bind:value={email}/>
    <button on:click="{() => {generateOtp(email)}}">Generate OTP</button>
</div>




<div class="flex flex-col align-middle align-middle justify-center text-center">
    Enter Your 6 digit OTP
</div>
<div class="flex flex-col align-middle justify-center text-box-div">
<div class="py-2 grid gap-2 grid-cols-1 md:grid-cols-6 align-middle justify-center text-center">
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
</div>
<span class="flex flex-col text-center align-middle justify-center">
    <input type="button" on:click="{verifyTheOtp}" name="Verify" value="Verify">
</span>
</div>