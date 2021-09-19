<script>
    import { createEventDispatcher } from 'svelte';
    import Frame from "./frame.svelte";
	import skins from "../data/skins.json"

    let frame = skins["frame"];
    let scenery = skins["scenery"];
    let castle = skins["castle"];

    const dispatch = createEventDispatcher();

    function updateFramePower(event) {
        dispatch('skin', {
            frame: event.detail.frame
        });
    }
</script>
<div class="skin">
    <Frame on:frame="{updateFramePower}" />
</div> 