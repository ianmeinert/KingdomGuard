<script>
    import { createEventDispatcher } from 'svelte';

    let power = {
      "slot": "",
      "owned": ""
    };
    
    const dispatch = createEventDispatcher();

    function updatePower() {
        dispatch('frame', {
            frame: power
        });
    }
</script>

<div>
    <h4>Frame Bonus</h4>
    <img src="images/skins/Frame.jpg" alt="Frame"/>
    <label for="slot">Stat Power:
        <input type="text" id="slot" name="slot" 
            bind:value={power.slot} on:change="{updatePower}">
    </label>
    <label for="owned">Total Owned Stat Power:
        <input type="text" id="owned" name="owned" 
            bind:value={power.owned} on:change="{updatePower}">
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