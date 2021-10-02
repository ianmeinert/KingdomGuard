<script>
    import { createEventDispatcher } from 'svelte';
    
    export let type;
    export let path;

    export let value;
    const dispatch = createEventDispatcher();

    function updateValue() {
        dispatch(type, {
            text: value,
            type: type
        });
    }

</script>
<div>
    <h4>{type}</h4>
    <img src="images/{path}/{type}.jpg" alt="{type}"/>
    <label for="value">
        Level: 
        <input type="text" id="level" name="level" bind:value={value} on:change="{updateValue}">
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