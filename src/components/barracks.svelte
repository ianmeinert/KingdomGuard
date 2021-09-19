<script>
    import { createEventDispatcher } from 'svelte';
    import tech from '../data/tech.json';
    
    const dispatch = createEventDispatcher();
    let barracks = tech.barracks;

    function updateArcher() {
        updatePower();
    }

    function updateFire() {
        updatePower();
    }

    function updateGoblin() {
        updatePower();
    }

    function updateIce() {
        updatePower();
    }

    function updatePower() {
        dispatch('barracks', {
            barracks: tech.barracks
        });
    }
</script>

<div>
    <h4>Barracks Bonus</h4>
    <img src="images/tech/Barracks.jpg" alt="Frame"/>
    <label for="archer">Archer Level:
        <input type="text" id="archer" name="archer"
            bind:value={barracks.archer} on:change="{updateArcher}">
    </label>
    <label for="fire">Fire Level
        <input type="text" id="fire" name="fire"
            bind:value={barracks.fire} on:change="{updateFire}">
    </label>
    <label for="goblin">Goblin Level
        <input type="text" id="goblin" name="goblin"
            bind:value={barracks.goblin} on:change="{updateGoblin}">
    </label>
    <label for="ice">Ice Level
        <input type="text" id="ice" name="ice"
            bind:value={barracks.ice} on:change="{updateIce}">
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