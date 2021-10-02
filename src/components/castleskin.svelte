<script>
    import { createEventDispatcher } from 'svelte';
    import Select from 'svelte-select';

    const types = ['Archer','Fire','Ice','Goblin','Overall'];

    let power = {
        "overall": "",
      "type": {
        "name": "",
        "percent": ""
      }
    };
    
    const dispatch = createEventDispatcher();

    function updateOverall() {
        updatePower();
    }

    function updateTypePercent(event) {
        updatePower();
    }

    function handleSelect(event) {
        var e = document.getElementById("hidden");
        e.style.display = "block";
        power.type.name = event.detail.value;
    }

    function handleClear() {
        var e = document.getElementById("hidden");
        e.style.display = "none"
        power.type.name = "";
        power.type.percent = "";
        updatePower();
    }

    function updatePower() {
        dispatch('castle', {
            castle: power
        });
    }
</script>
<div>
    <h4>Castle Bonus</h4>
    <img src="images/skins/Castle.jpg" alt="Castle"/>
    <label for="overall">Overall Power:
        <input type="text" id="overall" name="overall" 
            bind:value={power.overall} on:change="{updateOverall}">
    </label>
    
    <label for="types">Type Power:
        <Select id="types" items={types} on:select={handleSelect} on:clear={handleClear}></Select>        
    </label>
    <div id="hidden">
        <label for="percent">Percent
            <input type="text" id="percent" name="percent" 
                bind:value={power.type.percent} on:change="{updateTypePercent}">
        </label>
    </div>
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
    #hidden {
        display: none;
    }

</style>