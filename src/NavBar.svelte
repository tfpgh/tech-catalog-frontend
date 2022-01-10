<script>
    import Category from "./Category.svelte";

    export let categories = ["all"];
</script>

<div>
    {#each categories as category}
        <Category name={category} />
    {/each}
</div>

<style>
    div {
        position: fixed;
        display: flex;
        width: 100%;
        margin-left: 0px;
        top: 0px;
        left: 0px;
        height: 100px;
        background-color: #23272a;
        border-radius: 0 0 2rem 2rem;
    }
</style>
