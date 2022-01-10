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
        background-color: #f1faee;
        width: 380px;
        text-align: center;
        border-radius: 20px;
        border-style: solid;
        border-color: #457b9d;
        border-width: 3px;
        padding: 1%;
        padding-top: 0;
        margin: 1%;
    }

    h1 {
        color: #e63946;
    }

    p {
        color: #457b9d;
    }

    img {
        max-width: 95%;
        border-radius: 20px;
    }
</style>
