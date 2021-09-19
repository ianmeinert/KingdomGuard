<script>
    import { createEventDispatcher } from 'svelte';
    
    export let type;
    export let path;

    let level;
    const dispatch = createEventDispatcher();

    function updateLevel() {
        dispatch(type, {
            text: level,
            type: type
        });
    }

</script>
<div>
    <h4>{type}</h4>
    <img src="images/{path}/{type}.jpg" alt="{type}"/>
    <label for="level">
        Level: 
        <input type="text" id="level" name="level" bind:value={level} on:change="{updateLevel}">
    </label>
    
</div>
<style>
    div {
        width: 100%;
    }
    img {
        max-height: 100px;
        height: auto;
        border-radius: 10px 10px 10px 10px;
    }
    input {
        width: 50px;
    }
</style>