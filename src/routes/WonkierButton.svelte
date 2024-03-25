<script>
    import Container from "./Container.svelte";
	
    export let value = 0;
    let random = 0;
    let curr = "FizzBuzz";

    function handleClick() {
	    random = Math.floor(Math.random() * 10);
	    value += random;

        if (value % 3 == 0 && value % 5 == 0){
            curr = "FizzBuzz";
        }
        else if (value % 3 == 0){
            curr = "Fizz";
        }
        else if (value % 5 == 0){
            curr = "Buzz";
        }
        else {
            curr = "Default";
        }
    }

    let isDisabled = false;

    function toggleLock() {
        isDisabled = !isDisabled;
    }
    
</script>

<Container>
    <div data-testid="text-input" contenteditable bind:innerHTML={curr} />

    <button data-testid="lock-button" on:click={toggleLock}> 
        Lock
    </button>

    <button data-testid="wonkier-button" on:click={handleClick} class="{isDisabled ? 'locked' : curr}" disabled={isDisabled}> 
        {#if value % 3 == 0 && value % 5 == 0}
            {'FizzBuzz ' + value}
        {:else if value % 3 == 0}
            {'Fizz ' + value}
        {:else if value % 5 == 0}
            {'Buzz ' + value}
        {:else}
            {value}
        {/if}
    </button>

    {#if curr == "FizzBuzz"}
        <p> FizzBuzz! </p> 
    {/if}

</Container>

<style>
    [contenteditable] {
        padding: 0.5em;
        border: 1px solid #eee;
        border-radius: 4px;
    }
    button {
        margin: 1em;
        transform: rotate(0deg);
        transition: transform 0.5;
    }

    .Fizz {
        background-color: red;
        color: white;
    }

    .Buzz {
        background-color: green;
        color: white;
    }

    .FizzBuzz {
        background-color: blue;
        color: white;
    }

    .locked {
        text-decoration: line-through;
    }
</style>