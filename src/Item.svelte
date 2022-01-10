<script>
    export let key;
    export let name = "Default Name";
    export let desc = "Default Description";
    export let quantity = "42";
    export let image_url = "https://via.placeholder.com/720";

    function updateItem() {
        const item = {
            key: key,
            name: name,
            description: desc,
            quantity: quantity,
        };

        fetch("https://tech-catalog-backend.herokuapp.com/update_item", {
            method: "POST",
            headers: {
                "Content-Type": "application/json",
            },
            body: JSON.stringify(item),
        });
    }

    function deleteItem() {
        fetch(
            "https://tech-catalog-backend.herokuapp.com/delete_item?key=" + key,
            {
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                },
            }
        ).then(() => document.location.reload());
    }
</script>

<div on:input={updateItem}>
    <h1 contenteditable="true" bind:textContent={name}>{name}</h1>
    <p contenteditable="true" bind:textContent={desc}>{desc}</p>
    <p contenteditable="true" bind:textContent={quantity}>
        Quantity: {quantity}
    </p>
    <img src={image_url} alt={desc} />
    <button on:click={deleteItem}>Delete!</button>
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

    h1,
    button {
        color: #e63946;
    }

    button {
        width: 95%;
        margin-top: 3%;
        background-color: #eeeeee;
        border-radius: 20px;
    }

    p {
        color: #457b9d;
    }

    img {
        max-width: 95%;
        border-radius: 20px;
    }
</style>
