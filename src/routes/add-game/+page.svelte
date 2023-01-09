<script lang="ts">
    console.log('Loaded');


    let selectedFaction = '';
    
    let players = [{faction: '', playerName: ''}];

    let factions = [
        { name: 'Atreides', value: 'atreides' },
        { name: 'Harkonnen', value: 'harkonnen' },
        { name: 'Fremen', value: 'fremen' },
        { name: 'Emperor', value: 'emperor' },
        { name: 'Guild', value: 'guild' },
        { name: 'Bene Gesserit', value: 'bene-gesserit' }
    ]

    function addPlayer() {
        players = [...players, {faction: '', playerName: ''}];
    }

    function removePlayer(index: number) {
        players = players.filter((_, i) => i !== index);
    }

    $: activePlayers = players;

</script>


<form>
    <div class="container mt-4">
        <div class="row mb-3">
            <div class="col-3">
                <label for="datePlayed" class="form-label">Date</label>
                <input type="date" class="form-control" id="datePlayed" />
            </div>
        </div>
        <div class="row mb-3">
            <label class="form-label" for="players">Players</label>
            <div class="form-group">
                {#each activePlayers as player, index}
                    <div class="col-6">
                        <div class="input-group" id="player-1">
                            {#if player.faction}
                                <label class="input-group-text" for="faction-{index}">
                                    <img src="/images/factions/{player.faction}.png" style="width: 1.5rem; height: 1.5rem;" class="img-fluid" alt="none"/>
                                </label>
                            {/if}
                            <select class="form-select" id="faction-{index}" bind:value={player.faction}>
                                <option value="none" disabled hidden selected>Faction</option>
                                {#each factions as faction}
                                    <option value={faction.value}>{faction.name}</option>
                                {/each}
                            </select>
                            <input type="text" class="form-control" placeholder="Player name" />
                            <button class="btn btn-outline-danger" on:click={() => removePlayer(index)}>X</button>
                        </div>
                    </div>
                {/each}
                <button class="btn btn-outline-success" on:click={addPlayer}>+</button>
            </div>
        </div>
        <div class="row mb-3">
            <div class="col-6">
                <div class="form-floating">
                    <select class="form-select" id="winner">
                        <option value="Atreides">Atreides</option>
                        <option value="Harkonnen">Harkonnen</option>
                        <option value="Fremen">Fremen</option>
                        <option value="Emperor">Emperor</option>
                        <option value="Guild">Guild</option>
                        <option value="Bene Gesserit">Bene Gesserit</option>
                    </select>
                    <label for="winner" class="form-label">Winner</label>
                </div>
            </div>
    </div>
</form>