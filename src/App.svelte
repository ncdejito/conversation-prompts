<script>
    import Hoverable from "./Hoverable.svelte";
    import Modal from "./Modal.svelte";
    import { prompts, sources } from "./Prompts.js";
    let count = 0;

    let showModal = false;
    let Set = "Friends"; // ["Work", "Friends", "SO"];

    function handleClick() {
        count += 1;
    }
    function getRandomInt(min, max) {
        //The maximum is exclusive and the minimum is inclusive
        min = Math.ceil(min);
        max = Math.floor(max);
        return Math.floor(Math.random() * (max - min) + min);
    }

    function getPrompt(Set) {
        let max = Object.keys(prompts[Set]).length;
        let ind = getRandomInt(0, max);
        return prompts[Set][ind];
    }
</script>

<Hoverable let:hovering={active}>
    <div class:active>
        {#if active}
            <button
                on:click={() => {
                    showModal = true;
                    Set = "Work";
                }}
            >
                Small talk
            </button>
        {:else}
            <p>💼 Work</p>
        {/if}
    </div>
</Hoverable>

<Hoverable let:hovering={active}>
    <div class:active>
        {#if active}
            <button
                on:click={() => {
                    showModal = true;
                    Set = "Friends";
                }}
            >
                Deep talks
            </button>
        {:else}
            <p>👬 Friends</p>
        {/if}
    </div>
</Hoverable>

<Hoverable let:hovering={active}>
    <div class:active>
        {#if active}
            <button
                on:click={() => {
                    showModal = true;
                    Set = "Date";
                }}
            >
                Getting to know you
            </button>
        {:else}
            <p>❤️ Date</p>
        {/if}
    </div>
</Hoverable>

<Hoverable let:hovering={active}>
    <div class:active>
        {#if active}
            <p>👷 Under construction</p>
            <button on:click={handleClick}>
                I want it! {count}
            </button>
        {:else}
            <p>Input your own</p>
        {/if}
    </div>
</Hoverable>

{#if showModal}
    <Modal on:close={() => (showModal = false)}>
        <h2>{getPrompt(Set)}</h2>

        <a href={sources[Set]}>Source</a>
    </Modal>
{/if}

<style>
    div {
        padding: 1em;
        margin: 0 0 1em 0;
        background-color: #eee;
    }

    .active {
        background-color: #ff3e00;
        color: white;
    }
</style>
