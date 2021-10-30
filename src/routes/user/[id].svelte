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


    export async function add_candy() {
        let uri = `http://192.168.1.10:5000/add/candy?name=${candy_name}&flavour=${flavour}&given=${given_by}`
        const res1 = fetch(uri).then(response => response.json()).then(data => console.log(data));
    }


    let given_by = "";
    let candy_name = "";
    let flavour = "";


    import NewCandy from '../../components/new_candy.svelte';

</script>

<!-- {typeof(user)} -->


<div class="grid gap-4 md:grid-cols-2 grid-cols-1 align-middle justify-centre">
{#each  user["userdata"] as user_candy, i}
<!-- <br> -->
<Candies candies={[user_candy["name"], ...user_candy["givenby"]]} />
{/each}
</div>
<div>
<form>
    <input type="text" bind:value={given_by} />
    <input type="text" bind:value={candy_name} />
    <input type="text" bind:value={flavour} />
    <button on:click={add_candy}> Submit</button>
</form>
</div>

<!-- <NewCandy user={user} /> -->

<!-- // () => {
    // user["userdata"].push({
    //     "flavour": flavour,
    //     "name": candy_name,
    //     "givenby": given_by,

    // });
    // user = user; -->
