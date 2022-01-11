<script>
    export let name = "Default Name";
    export let description = "Default Description";
    export let quantity = "42";
    export let image_url = "https://via.placeholder.com/720";
</script>

<div>
    <h1 id="name">{name}</h1>
    <p id="description">{description}</p>
    <p id="quantity">Quantity: {quantity}</p>
    <img src={image_url} alt={description} />
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
