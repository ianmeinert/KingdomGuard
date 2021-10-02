<script>
	import { onMount } from 'svelte';
	import heros from "../data/heros.json";

    export let heroname; 
    export let dnlevel;
    let herolist = [];
    let hero = {};
    
    onMount(async () => {
		herolist = heros.filter(
            function(heros){ return heros.name == heroname }
        );
        hero = herolist[0];
	});
   
</script>

{#if hero && hero.name && hero.type}
<p><img src="/images/type/{hero.type}.png" alt="{hero.type}" width="25px"/>Bonus {dnlevel}%</p>
<img src="/images/hero/{hero.name}Hero.png" alt="{hero.name}" />
<h3>{hero.category} {hero.name} ({hero.type})</h3>

<pre>
Unit Base           : {hero.stats.unit.base || "9,999,999,999"}
Unit Evolution      : {hero.stats.unit.evolution || "9,999,999,999"}
Unit Talent         : {hero.stats.unit.talent || "9,999,999,999"}
Hero Base           : {hero.stats.hero.base || "9,999,999,999"}
Hero Star           : {hero.stats.hero.star || "9,999,999,999"}
Hero Skill          : {hero.stats.hero.skill || "9,999,999,999"}
Dragon Power        : {hero.stats.power.dragon || "9,999,999,999"}
Tech Power          : {hero.stats.power.tech || "9,999,999,999"}
Bonds Power         : {hero.stats.power.bonds || "9,999,999,999"}
Skin Power          : {hero.stats.power.skin || "9,999,999,999"}
Alliance Bldg Power : {hero.stats.power.alliancebldg || "9,999,999,999"}
VIP Power           : {hero.stats.power.vip || "9,999,999,999"}
Total Attack Power  : {hero.stats.power.totalattack || "9,999,999,999"}
</pre>
{/if}