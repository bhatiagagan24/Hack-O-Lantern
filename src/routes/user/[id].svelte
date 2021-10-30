<script context="module">
// id is email here
// this page is for route /user/emailid

// On page loadup, I will verify the result from the writable. 
// This page will only be visible if writable says loggedin




 export async function load({page}) {



    const email = page.params.id;
    console.log("email received -> ", email);

    // user details will be fetched here using a get request to the API.
    // then those will be passed down as props
    
    const uri = `http://192.168.1.10:5000/getdata?email=${email}`
    var candy_resp = [];
    const resp = await fetch(uri).then(response => response.json()).then(data => {
        for(var i= 0; i<data.length; i++) {
            candy_resp.push(data[i]);
        }
    });
    console.log("candyresp" , candy_resp);


    return {props: {
        user: {"email": `${email}` , "userdata": candy_resp}
    }
};
}

</script>

<!-- 
// Redirecting not working to home page when not signedin

    async function signinredirect() {
        if(!isLoggedin) {
            console.log("Redirecting");
        return {
            headers: {Location: '/'},
            status: 302
            } 
        } else {
            console.log("Not redirecting")
        }
    }
    signinredirect();

    // The code between this comment and the comment above does not work. Fix the redirect bug -->


<script>

    import { userDetails } from "../../stores/user.js";

import Candies from "../../components/candies.svelte";

    const userEmail = $userDetails["email"];
    const isLoggedin = $userDetails["loggedin"];
    
    console.log("userdetails type -> ", typeof($userDetails));

    console.log("ue -> ", userEmail);

    // console.log(`userDeatils -> , ${typeof($userDetails)}`);

    export let user;
    console.log(typeof(user));
    console.log(user);  
    console.log(user["email"]);
    console.log(user["userdata"][0]["flavour"]); 

    let user_candy_list = [];

    user["userdata"].forEach(()=> {
        user_candy_list.push(user["userdata"]["name"]);
    })

    console.log("user_candy_list -> ", user_candy_list);

    var json_resp_length = user["userdata"].length;
    console.log(json_resp_length);

</script>

<!-- {typeof(user)} -->


<div class="grid gap-4 md:grid-cols-2 grid-cols-1 align-middle justify-centre">
{#each  user["userdata"] as user_candy, i}
<!-- <br> -->
<Candies candies={[user_candy["name"], ...user_candy["givenby"]]} />
{/each}
</div>

<div class="align-middle justify-center text-center py-10">
    <button style="color:white; background-color:black; width:10em" class="rounded-md hover:shadow-md">New Candy</button>
</div>