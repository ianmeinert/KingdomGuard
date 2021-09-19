<script>
    import { createEventDispatcher } from 'svelte';
    import techjson from '../data/tech.json';
    import Input from "./input.svelte";
    import Academy from "./academy.svelte";
    import Barracks from "./barracks.svelte";

    const dispatch = createEventDispatcher();

    let tech = techjson;

    function updateDragonPower(event) {
        tech.dragon = event.detail.text;
        updateTech()
    }
    function updateAcademyPower(event) {
        tech.academy = event.detail.academy;
        updateTech()
    }
    function updateBarracksPower(event) {
        tech.barracks = event.detail.barracks;
        updateTech()
    }

    function updateTech() {
        dispatch('tech', {
            tech: tech
        });
    }

</script>
<div class="skincontainer">
    <div class="skin">
        <Input type="Dragon" path="tech" on:Dragon="{updateDragonPower}" />
    </div>
    <div class="skin">
        <Academy on:academy="{updateAcademyPower}" />
    </div>
    <div class="skin">
        <Barracks on:barracks="{updateBarracksPower}" />
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