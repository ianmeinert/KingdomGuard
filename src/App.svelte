<script>
	import dragonnests from "./data/dragonnests.json"
	import heros from "./data/heros.json";
	import Dragonnest from "./components/dragonnest.svelte";
	import Hero from "./components/hero.svelte";
	import Select from 'svelte-select'
	import Skin from "./components/skin.svelte";
	
	let dnlist = dragonnests;
	let selected;
	let skin;
	
	const groupBy = (hero) => hero.type;
	const optionIdentifier = 'name';
	const getOptionLabel = (hero) => hero.name + " ("+hero.category+")";
	const getSelectionLabel = (hero) => hero.name + " ("+hero.category+")";

	function handleSelect(event) {
		selected = event.detail;
	}

	function handleSkin(event) {
		skin = event.detail.frame;
		console.log(skin);
	}

	function handleLevel(event) {
		let dnIncoming = {
			"type":event.detail.type,
			"level":event.detail.text
		}

		const searchIndex = dnlist.findIndex((dn) => dn.type == dnIncoming.type);
		console.log(searchIndex);

		dnlist.forEach(item => {
					console.log("in foreach");
					if (item.type == dnIncoming.type)  {
						console.log("type found");
						item.level = dnIncoming.level;
					}
				});	

		dnlist = dnlist;
	}

</script>

<main>
	<div class="header">
		<h1>Kingdom Guard</h1>
		<h2>Hero Bond Calculator</h2>
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
		<div class="skin">
			<Skin on:skin={handleSkin}/>
		</div>
	</div>

	<div class="herocontainer container">
		<h3>Hero Selection:</h3>
		<img src="/images/heros.jpg" alt="Heros group shot" width = "500"/>
		<label for="heros">Choose your heros:</label>
		<Select items={heros} {groupBy} {optionIdentifier} {getSelectionLabel} {getOptionLabel} 
			isMulti={true} on:select={handleSelect} ></Select>
		
		{#if selected}
			{#each selected as s}
				<div class="hero">
				{#each dnlist as dn}
					{#if dn.type == s.type}
					<Hero dnlevel={dn.level} heroname={s.name} category={s.category} type={s.type} />
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
	div.header {
		background-image: url("/images/HeroesBounds.png");
		background-repeat: no-repeat;
		background-position: center;
		background-size:contain;
		opacity: 0.60;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight:300;
	}

	h2 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 3em;
		font-weight: 100;
	}

	h3 {
		color:chocolate;
		font-size: 2em;
		font-weight: 100;
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

	.skin {
		float: left;
  		width: 33%;
	}

	.skincontainer:after {
		content: "";
		display: table;
		clear: both;
		width: 500px;
	}

	label {
		text-align:left;
		margin: 0 0 10px;
	}

</style>