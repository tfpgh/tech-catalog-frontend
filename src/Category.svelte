<script>
    export let name = "";
    export let active = false;
</script>

<button id={name} on:click class:active>{name}</button>

<style>
    button {
        background-color: var(--background-color);
        font-family: var(--secondary-font);
        height: 3rem;
        color: var(--main-text-color);
        min-width: 6rem;
        font-size: 1.2rem;
        padding: 0px 10px;
        border-radius: var(--corner-radius);
        border: 3px solid var(--border-color);
    }

    button:hover {
        border-color: var(--main-text-color);
    }

    .active {
        background-color: var(--border-color);
        color: var(--background-color);
    }
</style>
