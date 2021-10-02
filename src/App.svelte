<script>
	import Select from "svelte-select";
	import dragonnests from "./data/dragonnests.json";
	import heros from "./data/heros.json";
	import Dragonnest from "./components/dragonnest.svelte";
	import Hero from "./components/hero.svelte";
	import Skin from "./components/skin.svelte";
	import Tech from "./components/tech.svelte";
	import Castle from "./components/castle.svelte";

	let dnlist = dragonnests;
	let selected;
	let skins;
	let tech;
	let castlelevel;

	const groupBy = (hero) => hero.type;
	const optionIdentifier = "name";
	const getOptionLabel = (hero) => hero.name + " (" + hero.category + ")";
	const getSelectionLabel = (hero) => hero.name + " (" + hero.category + ")";

	function handleSelect(event) {
		selected = event.detail;
	}

	function handleSkin(event) {
		skins = event.detail.skins;
	}

	function handleTech(event) {
		tech = event.detail.tech;
	}

	function handleLevel(event) {
		let dnIncoming = {
			type: event.detail.type,
			level: event.detail.text,
		};

		dnlist.forEach((item) => {
			if (item.type == dnIncoming.type) {
				item.level = dnIncoming.level;
			}
		});

		dnlist = dnlist;
	}
</script>

<main>
	<div id="header">
		<h1>Kingdom Guard</h1>
		<h2>Hero Bond Calculator</h2>
		<p class="isa_info">
			***This is still under development. Calculations are not implemented
			yet.***
		</p>
		<div id="links">
			| <a
				href="https://github.com/ianmeinert/KingdomGuard/issues"
				target="_blank"
				rel="noopener">Find a bug?</a
			>
			|
			<a
				href="https://cash.app/$PogLife4Me"
				target="_blank"
				rel="noopener"
			>
				<img src="/images/CashApp.jpg" alt="CashApp" width="15px" />
				CashApp</a
			> |
		</div>
	</div>

	<div class="container castlecontainer">
		<h3>Castle Level</h3>
		<div>
			<Castle bind:value={castlelevel} />
		</div>
	</div>

	<div class="container dncontainer">
		<h3>Dragon Nest Bonus:</h3>
		{#each dnlist as dn}
			<div class="dn">
				<Dragonnest type={dn.type} on:level={handleLevel} />
				<p>{dn.type}: {dn.level}%</p>
			</div>
		{/each}
	</div>

	<div class="skincontainer container">
		<h3>Skin Bonus:</h3>
		<div>
			<Skin on:skin={handleSkin} />
		</div>
	</div>

	<div class="techcontainer container">
		<h3>Tech Bonus:</h3>
		<div>
			<Tech on:tech={handleTech} />
		</div>
	</div>

	<div class="herocontainer container">
		<h3>Hero Selection:</h3>
		<img src="/images/heros.jpg" alt="Heros group shot" width="500" />
		<label for="heros">Choose your heros:</label>
		<Select
			items={heros}
			{groupBy}
			{optionIdentifier}
			{getSelectionLabel}
			{getOptionLabel}
			isMulti={true}
			on:select={handleSelect}
		/>

		{#if selected}
			{#each selected as s}
				<div class="hero">
					{#each dnlist as dn}
						{#if dn.type == s.type}
							<Hero dnlevel={dn.level} heroname={s.name} />
						{/if}
					{/each}
				</div>
			{/each}
		{/if}
	</div>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 1024px;
		min-height: 1250px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 300;
	}

	h2 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 3em;
		font-weight: 100;
	}

	h3 {
		color: chocolate;
		font-size: 2em;
		font-weight: 100;
	}

	#header {
		padding-bottom: 25px;
	}

	#links {
		float: right;
	}

	.dn {
		float: left;
		width: 25%;
	}
	.container {
		border: 3px solid chocolate;
		margin-bottom: 25px;
	}

	.dncontainer:after {
		content: "";
		display: table;
		clear: both;
	}

	.hero {
		float: left;
		width: auto;
		padding: 25px;
	}

	.herocontainer:after {
		content: "";
		display: table;
		clear: both;
		width: 500px;
	}

	.herocontainer div img {
		object-fit: cover;
	}

	label {
		text-align: left;
		margin: 0 0 10px;
	}

	img {
		border-radius: 10px 10px 10px 10px;
	}

	.isa_info {
		color: #00529b;
		background-color: #bde5f8;
		margin: 10px 0px;
		padding: 12px;
	}
</style>
