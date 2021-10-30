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
    <button on:click="{generateOtp}">Generate OTP</button>
</div>

{otp_recieved}


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