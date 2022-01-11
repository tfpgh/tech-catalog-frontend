<script>
	import Item from "./Item.svelte";
	import { onMount } from "svelte";

	function toTitleCase(string) {
		return string
			.toLowerCase()
			.split(" ")
			.map((word) => {
				return word.charAt(0).toUpperCase() + word.slice(1);
			})
			.join(" ");
	}

	let items = [];
	let categories = [];
	$: {
		let generating_categories = [];
		items.forEach((item) => {
			item.categories = item.categories.split(", ");
			item.categories.forEach((category) => {
				if (!generating_categories.includes(toTitleCase(category))) {
					generating_categories.push(toTitleCase(category));
				}
			});
		});

		categories = generating_categories;
	}
	onMount(async () => {
		// Get items
		const res = await fetch(
			`https://tech-catalog-backend.herokuapp.com/get_items`
		);
		items = await res.json();

		// Assign theme if necessary
		if (localStorage.getItem("theme") === null) {
			localStorage.setItem("theme", Math.floor(Math.random() * 3) + 1);
		}
	});
</script>

<main>
	{#each items as item}
		<Item
			name={item.name}
			description={item.description}
			quantity={item.quantity}
			image_url={"https://tech-catalog-images.s3.us-west-1.amazonaws.com/" +
				item.key +
				".png"}
		/>
	{/each}
</main>

<style>
	:global(body) {
		background-color: #eeeeee;
	}

	main {
		display: flex;
		flex-wrap: wrap;
		flex-shrink: 1;
		justify-content: center;
	}
</style>
