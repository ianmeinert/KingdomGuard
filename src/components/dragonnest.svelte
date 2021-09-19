<script>
    import { createEventDispatcher } from 'svelte';
    
    export let type 

    let level
    const dispatch = createEventDispatcher();

    function updateLevel() {
        dispatch('level', {
            text: level,
            type: type
        });
    }

</script>
<div>
    <h4>{type} Dragon Nest</h4>
    <img src="images/DragonNest.jpg" alt="dragon nest"/>
    <label for="dnlevel">
        Combined level: 
        <input type="text" id="dnlevel" name="dnlevel" bind:value={level} on:change="{updateLevel}">
    </label>
    
</div>
<style>
    div {
        width: 100%;
    }
    img {
        max-width: 100px;
        height: auto;
    }
    input {
        width: 50px;
    }
</style>