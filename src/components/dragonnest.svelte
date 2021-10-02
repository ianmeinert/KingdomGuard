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
    <img src="images/alliance/DragonNest.jpg" alt="dragon nest"/>
    <img class="top" src="images/type/{type}.png" alt="dragon nest type"/>
    <label for="dnlevel">
        Combined level: 
        <input type="text" id="dnlevel" name="dnlevel" bind:value={level} on:change="{updateLevel}">
    </label>
    
</div>
<style>
    div {
        position:relative;
        width: 100%;
    }
    img {
        max-height: 100px;
        height: auto;
        border-radius: 10px 10px 10px 10px;
    }

    img.top {
        position: absolute;
        top: 25px;
        left: 50px;
        height: 40px;
    }

    input {
        width: 50px;
    }
</style>