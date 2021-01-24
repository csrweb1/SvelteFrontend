<script>
import { bind } from "svelte/internal";
    let email = "";
    let password = "";
    let isLoading = false;
    let isSuccess = false;
    let errors = 'error would go here, instead i posted the data to a random url and it prints that instead';
    
    async function handleSubmit () {
        isLoading = true
		const res = await fetch('https://httpbin.org/post', {
			method: 'POST',
			body: JSON.stringify({
				email,
				password
			})
		})
		
		const json = await res.json()
        errors = JSON.stringify(json)
        isLoading = false
	}
</script>

<style>
    /* list-input */
    input[type=text] {
        padding: 5px;
        margin: 0 10px;
        border: 2px solid #ced4da;
        border-radius: 4px;
    }

    /* list-stats */

    /* list-item */

    /* any item (used by list-item, list-input, list-stats */
    .item {
    display: inline-flex;
    flex-direction: row;
    align-items: center;
    margin: 5px;
    padding: 12px 0 10px 10px;
    background-color: #e9ecef;
    box-shadow: 3px 3px 10px #e9ecef;
    border-radius: 4px;
    overflow: hidden;
    transition: transform 0.1s ease-in-out;
    }

    .item:hover {
    transform: translateY(-3px) scale(1.02);
    box-shadow: 3px 3px 10px #d0ebff;
    transition: all 0.1s ease-in-out;
    }

    .item label {
    margin-bottom: 5px;
    padding-left: 9px;
    }
    .button{
    display:inline-block;
    padding:0.35em 1.2em;
    border:0.1em solid #FFFFFF;
    margin:0 0.3em 0.3em 0;
    border-radius:0.12em;
    box-sizing: border-box;
    text-decoration:none;
    font-family:'Roboto',sans-serif;
    font-weight:300;
    color:#000000;
    text-align:center;
    transition: all 0.2s;
    }
    .button:hover {
    color:#FFFFFF;
    background-color:#000000;
    }
</style>
<center>
    <h1>Login</h1>
        <form on:submit|preventDefault={handleSubmit}>
            {#if isSuccess}
                <div class="success">
                    🔓
                    <br />
                    You've been successfully logged in.
                </div>
            {:else}
            <div class="item">
                <label>Name</label>
                <input type="text" bind:value={email} />
            </div>
            <div>{errors}</div>
            <div class="item">
                <label>E-mail</label>
                <input type="text" bind:value={password}/>
            </div>
            <div></div>
            <button class="button" type="submit">{#if isLoading}Logging in...{:else}Log in 🔒{/if}</button>
            {/if}
        </form>
</center>
