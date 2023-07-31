<script lang="ts">
    import { fade } from "svelte/transition";

    let hasRolled = false;
    let dice1 = 0;
    let dice2 = 0;

    // Value used to always trigger transition in `key` block.
    let transitionTrigger = false;

    function rollDie(sides: number): number {
        return Math.floor(Math.random() * sides + 1);
    }

    function roll() {
        hasRolled = true;
        transitionTrigger = !transitionTrigger;
        dice1 = rollDie(6);
        dice2 = rollDie(6);
    }

    $: total = dice1 + dice2;
</script>

<main>
    <h1>Dice Roller</h1>

    {#key transitionTrigger}
        <div
            id="results"
            style:visibility={hasRolled ? "visible" : "hidden"}
            in:fade
        >
            <p id="dice-breakdown">{[dice1, dice2].join(" + ")}</p>
            <p id="total">{total}</p>
        </div>
    {/key}

    <button on:click={roll}> Roll </button>
</main>

<style>
    h1 {
        font-size: 3.2em;
        font-weight: 600;
        margin: 1.5rem;
    }

    button {
        border-radius: 8px;
        border: 1px solid transparent;
        padding: 0.6em 1.2em;
        font-size: 1em;
        font-weight: 500;
        font-family: inherit;
        color: rgba(255, 255, 255, 0.87);
        background-color: #1a1a1a;
        cursor: pointer;
        transition: border-color 0.25s;
    }
    button:hover {
        border-color: #646cff;
    }
    button:focus,
    button:focus-visible {
        outline: 4px auto -webkit-focus-ring-color;
    }

    #dice-breakdown {
        color: #aaaaaa;
        font-size: 1.25rem;
        margin-bottom: 0.5rem;
    }

    #total {
        font-size: 2.5rem;
        font-weight: 600;
        margin-bottom: 1.5rem;
    }
</style>
