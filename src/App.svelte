<script>
	import Item from "./Item.svelte";
	import NavBar from "./NavBar.svelte";
	import { onMount } from "svelte";

	let items = [];
	onMount(async () => {
		const res = await fetch(
			`https://tech-catalog-backend.herokuapp.com/get_items`
		);
		items = await res.json();
	});
</script>

<NavBar />
<main>
	{#each items as item}
		<Item
			{...item}
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
		margin: 100px;
		display: flex;
		flex-wrap: wrap;
		flex-shrink: 1;
		justify-content: center;
	}
</style>
