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
    const resp = await fetch(uri).then(response => response.json()).then(data => console.log(data));

    return {props: {
        title: `{"email": "${email}"}`
    }
};
}

</script>


<script>

    import { userDetails } from "../../stores/user.js";
    import { goto } from "$app/navigation";


    const userEmail = $userDetails["email"];
    const isLoggedin = $userDetails["loggedin"];
    
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

    // The code between this comment and the comment above does not work. Fix the redirect bug


    console.log("type -> ", typeof($userDetails));

    console.log("ue -> ", userEmail);

    // console.log(`userDeatils -> , ${typeof($userDetails)}`);

    export let title;

   
    


    var new_title = JSON.parse(title);
    // new_title = JSON.parse(new_title);
</script>

{new_title["email"]}
{typeof(title)}