<script>
    import { createEventDispatcher } from 'svelte';
	import skins from "../data/skins.json";
    import Frame from "./frame.svelte";
    import Castle from "./castle.svelte";
    import Input from "./input.svelte";

    const dispatch = createEventDispatcher();

    function updateFramePower(event) {
        skins.frame = event.detail.frame;
        updateSkins();
    }
    function updateSceneryPower(event) {
        skins.scenery = event.detail.text;
        updateSkins();
    }
    function updateCastlePower(event) {
        skins.castle = event.detail.castle;
        updateSkins();
    }

    function updateSkins() {
        dispatch('skin', {
            skins: skins
        });
    }

</script>
<div class="skincontainer">
    <div class="skin">
        <Frame on:frame="{updateFramePower}" />
    </div>
    <div class="skin">
        <Input type="Scenery" path="skins" on:Scenery="{updateSceneryPower}" />
    </div>
    <div class="skin">
        <Castle on:castle="{updateCastlePower}" />
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