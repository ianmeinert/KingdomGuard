<script>
    import { createEventDispatcher, onMount, setContext, getContext  } from 'svelte';
    import techjson from '../data/tech.json';
    import Input from "./input.svelte";
    import Academy from "./academy.svelte";
    import Barracks from "./barracks.svelte";

    let tech = techjson;
    const dispatch = createEventDispatcher();

    onMount(async () => {
        types = ["Fire","Ice","Archer","Goblin"];
        tech.troops = []
        types.forEach( type => {     
            let troop = {
                "text":"",
                "academy":"",
                "barracks": {
                    "talent":"",
                    "level":""
                }
            };       
            troop.text = type;
            tech.troops.push(troop)
        });
    });

    function updateTech() {
        dispatch('tech', {
            tech: tech
        });
    }

</script>
<div class="skincontainer">
    <div class="skin">
        <Input bind:value={tech.dragon} type="Dragon" path="tech" on:Dragon="{updateTech}" />
    </div>
    <div class="skin">
        <!-- <Academy bind:value={tech.troops} on:academy="{updateTech}" /> -->
    </div>
    <div class="skin">
        <Barracks bind:troops={tech.troops}/>
    </div>
</div> 

<style>
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
</style>