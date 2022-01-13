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

	let nav_bar_height = 58;

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

	localStorage.setItem("measurement_id", measurement_id);

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

		let cleaned_categories = generating_categories.filter((category) => {
			if (category === "All" || category === "Other") {
				return false;
			}
			return true;
		});

		cleaned_categories.sort();
		cleaned_categories.unshift("All"); // Makes sure all is at the begining
		cleaned_categories.push("Other"); // Makes sure other is at the end

		categories = cleaned_categories;
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

	window.dataLayer = window.dataLayer || [];
	function gtag() {
		dataLayer.push(arguments);
	}

	gtag("js", new Date());

	gtag("config", localStorage.getItem("measurement_id"));

	function switch_category(category) {
		category = category.toLowerCase();

		shown_category = category;
		gtag("event", "switch_category", {
			category: category,
		});
	}
</script>

<svelte:head>
	<title>Logan Tech Catalog Theme {theme}</title>
	<script
		async
		src="https://www.googletagmanager.com/gtag/js?id={measurement_id}"></script>
</svelte:head>

<div id="top" class="defaults theme-1">
	<div id="nav-bar" bind:clientHeight={nav_bar_height}>
		{#each categories as category}
			<Category
				name={category}
				active={shown_category === category.toLowerCase()}
				on:click={switch_category(category)}
			/>
		{/each}
	</div>
	<main style="padding-top: {nav_bar_height}px">
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
		min-height: 100vh;
	}

	main {
		display: flex;
		flex-wrap: wrap;
		flex-shrink: 1;
		justify-content: center;
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
		padding: 10px 15px;
		border-bottom: 3px solid var(--border-color);
	}
</style>
