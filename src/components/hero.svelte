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
{/if}