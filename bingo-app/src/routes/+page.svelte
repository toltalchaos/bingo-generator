<script>
    // @ts-nocheck
    import { onMount } from 'svelte';
    let textFields = [];
    let textFieldsString = '-create \n- a \n-dash seperated \n-list \n-of \n-text \n-fields \n-and \n-click \nthe \nbutton \nbelow \nto \nupdate \nthe \nbingo \ncard \nwith \nthe \nnew \nfields \n-';
    let bingoCard = [];

    function generateBingoCard() {
        // Randomize the text fields
        const randomizedFields = shuffle(textFields);
        // Split the text fields into rows
        const rows = chunk(randomizedFields, 5);
        // Create the bingo card
        bingoCard = rows;
    }

    function shuffle(array) {
        // Implementation of Fisher-Yates shuffle algorithm
        let currentIndex = array.length, temporaryValue, randomIndex;
        while (currentIndex !== 0) {
            randomIndex = Math.floor(Math.random() * currentIndex);
            currentIndex -= 1;
            temporaryValue = array[currentIndex];
            array[currentIndex] = array[randomIndex];
            array[randomIndex] = temporaryValue;
        }
        return array;
    }

    function chunk(array, size) {
        const chunkedArray = [];
        let index = 0;
        while (index < 25 ) {
            chunkedArray.push(array.slice(index, index + size));
            index += size;
        }
        return chunkedArray;
    }

    function updateTextFields() {
        textFields = textFieldsString.split('-').map(field => field.trim());
        generateBingoCard();
    }

    onMount(() => {
        // Initialize the text fields with some example values
        textFields = ['Field 1', 'Field 2', 'Field 3', 'Field 4', 'Field 5', 'Field 6', 'Field 7', 'Field 8', 'Field 9', 'Field 10', 'field 11', 'field 12', 'field 13', 'field 14', 'field 15', 'field 16', 'field 17', 'field 18', 'field 19', 'field 20', 'field 21', 'field 22', 'field 23', 'field 24', 'field 25'];
        generateBingoCard();
    });
</script>

<h2>Enter Text Fields</h2>
<textarea class="input-area" bind:value={textFieldsString}></textarea><hr/>
<button on:click={updateTextFields}>Update Text Fields</button>
<hr>
<button on:click={generateBingoCard}>Generate Bingo Card</button>
<div class="bingo-cards">
    {#if bingoCard.length > 0}
    <h2>Bingo Card</h2>
    {#each bingoCard as row}
        <div class="row">
            {#each row as field}
                <div class="field">{field}</div>
            {/each}
        </div>
    {/each}
{/if}
</div>


<style>
    .input-area {
        width: 100%;
        height: 10rem;
    }
    .row {
        display: flex;
    }

    .field {
        border: 1px solid black;
        width: 8rem;
        height: 5rem;
        padding: 10px;
        margin: 0px;
    }
</style>
