<script>
    import Container from "./Container.svelte";
	
    export let value = 0;
    let random = 0;
    let curr = "FizzBuzz";
    let text = "FizzBuzz" + value.toString();

    function handleClick() {
	    random = Math.floor(Math.random() * 10);
	    value += random;

        if (value % 3 == 0 && value % 5 == 0){
            curr = "FizzBuzz";
            text = "FizzBuzz " + value.toString();
        }
        else if (value % 3 == 0){
            curr = "Fizz";
            text = "Fizz " + value.toString();
        }
        else if (value % 5 == 0){
            curr = "Buzz";
            text = "Buzz " + value.toString();
        }
        else {
            curr = "Default";
            text = value.toString();
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
        {#if curr == "FizzBuzz"}
            {'FizzBuzz ' + value}
        {:else if curr == "Fizz"}
            {'Fizz ' + value}
        {:else if curr == "Buzz"}
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