<script>
    export let name = "";

    let promise = async function () {
        let promise = await fetch(`https://www.boredapi.com/api/activity`);
        if (promise.ok) {
            let response = await promise.json()
            return response.activity;
        } else {
            return "Sorry, I have no idea what you could do!"
        }
    }
</script>

<main>
    What's your name? <input type="text" bind:value={name} autofocus="autofocus"/>

    {#if name !== ""}
        <h1>Hello {name}!</h1>

        {#if name === "Jocke"}
            <h2>Ah, the curious one!</h2>
        {/if}

        <h3>Why not...</h3>
        {#await promise() then value}
            <p>{value}</p>
        {/await}
    {/if}
</main>

<style>
    main {
        text-align: center;
        padding: 1em;
        max-width: 240px;
        margin: 0 auto;
    }

    h1 {
        color: #ff3e00;
        text-transform: uppercase;
        font-size: 4em;
        font-weight: 100;
    }

    @media (min-width: 640px) {
        main {
            max-width: none;
        }
    }
</style>