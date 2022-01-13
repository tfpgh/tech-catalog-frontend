<script>
    export let name = "Default Name";
    export let description = "Default Description";
    export let quantity = "42";
    export let image_url = "https://via.placeholder.com/720";
</script>

<div>
    <h1 id="name" class="flex-basis-100 margin-tb">{name}</h1>
    <p id="description" class="flex-basis-100 margin-tb">{description}</p>
    <p id="quantity" class="flex-basis-100 margin-tb">
        Quantity: {quantity}
    </p>
    <img src={image_url} alt={description} class="flex-basis-100 margin-tb" />
</div>

<style>
    div {
        background-color: var(--secondary-background-color);
        width: 380px;
        text-align: center;
        border-radius: var(--corner-radius);
        border-style: solid;
        border-color: var(--border-color);
        border-width: 3px;
        padding: 15px;
        padding-bottom: 20px;
        padding-top: 0;
        margin: 15px;
        flex-grow: 1;
        display: flex;
        flex-wrap: wrap;
        align-items: center;
        justify-content: center;
    }

    .flex-basis-100 {
        flex-basis: 100%;
    }

    .margin-tb {
        margin-top: 0.4rem;
        margin-bottom: 0.4rem;
    }

    h1 {
        color: var(--main-text-color);
        font-family: var(--main-font);
    }

    p {
        color: var(--secondary-text-color);
        font-family: var(--secondary-font);
    }

    img {
        max-width: 95%;
        border-radius: var(--corner-radius);
    }
</style>
