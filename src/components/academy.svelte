<script>    
    export let tech;
</script>

<div>
    <h4>Academy Bonus</h4>

    <img src="images/tech/Academy.jpg" alt="Frame"/>
    <div class="divTable">
        <div class="divTableBody">
            <div class="divTableRow">
                <div class="divTableCell">&nbsp;</div>
                <div class="divTableCell">Bonus</div>
            </div>
            {#each tech.troops as troop}
                <div class="divTableRow">
                    <div class="divTableCell">{troop.text}</div>
                    <div class="divTableCell">
                        <input type="text" id="{troop.text}talent" name="{troop.text}talent"
                            bind:value="{troop.academy}">
                    </div>
                </div>
            {/each}
            <div class="divTableRow">
                <div class="divTableCell">Troop Capacity</div>
                <div class="divTableCell">
                    <input type="text" id="capacity" name="capacity"
                        bind:value="{tech.capacity}">
                </div>
            </div>   
        </div>
    </div>
</div>
<style>
    img {
        max-height: 100px;
        height: auto;
        border-radius: 10px 10px 10px 10px;
    }
    input {
        width: 50px;
    }

    .divTable{
        display: table;
        width: 100%;
    }

    .divTableRow {
        display: table-row;
    }

    .divTableCell {
        display: table-cell;
        padding: 3px 10px;
    }

    .divTableBody {
        display: table-row-group;
    }
</style>