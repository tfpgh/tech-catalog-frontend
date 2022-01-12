<script>
	import Item from "./Item.svelte";
	import Category from "./Category.svelte";
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
	let theme = localStorage.getItem("theme");

	// Assign theme if necessary
	if (theme === null) {
		theme = Math.floor(Math.random() * 3) + 1; // 1-3
		localStorage.setItem("theme", theme);
	}

	var measurement_id = "G-9RBCKH0VZC";

	if (theme === "2") {
		measurement_id = "G-M1C33DTF1P";
	} else if (theme === "3") {
		measurement_id = "G-EK34GRCELG";
	}

	let shown_category = "all";

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
			"https://tech-catalog-backend.herokuapp.com/get_items"
		);
		items = await res.json();

		if (theme != "1") {
			const top = document.getElementById("top");

			top.classList.add("theme-" + theme);
			top.classList.remove("theme-1");
		}
	});
</script>

<svelte:head>
	<script
		async
		src="https://www.googletagmanager.com/gtag/js?id={measurement_id}"></script>
	<script>
		window.dataLayer = window.dataLayer || [];
		function gtag() {
			dataLayer.push(arguments);
		}
		gtag("js", new Date());

		gtag("config", { measurement_id });
	</script>
</svelte:head>
<div id="top" class="defaults theme-1">
	<div id="nav-bar">
		{#each categories as category}
			<Category
				name={category}
				active={shown_category === category.toLowerCase()}
				on:click={() => (shown_category = category.toLowerCase())}
			/>
		{/each}
	</div>
	<main>
		{#each items as item}
			{#if item.categories.includes(shown_category)}
				<Item
					name={item.name}
					description={item.description}
					quantity={item.quantity}
					image_url={"https://tech-catalog-images.s3.us-west-1.amazonaws.com/" +
						item.key +
						".png"}
				/>
			{/if}
		{/each}
	</main>
</div>

<style>
	:global(body) {
		margin: 0px;
	}

	#top {
		background-color: var(--background-color);
	}

	main {
		display: flex;
		flex-wrap: wrap;
		flex-shrink: 1;
		justify-content: center;
		padding-top: 50px;
	}

	#nav-bar {
		display: flex;
		position: fixed;
		top: 0px;
		left: 0px;
		width: 100%;
		gap: 15px;
		align-items: center;
		background-color: var(--header-background-color);
		flex-wrap: wrap;
		padding: 5px 15px;
	}
</style>
