<script>
    let lastResult = "";
    let display = "";

    function addToCalcul() {
        display += event.target.innerText;
    }

    function clearCalcul() {
        display = "";
    }

    function delFromCalcul() {
        display = display.slice(0, -1);
    }

    function getResult() {
        lastResult = eval(display);
        console.log(lastResult);
        display = "";
    }
</script>

<form>
    <div class="display">
        <p class="lastResult">
            {#if lastResult}
                {lastResult}
            {:else}
                &nbsp;
            {/if}
        </p>
        <p>
            {#if display}
                {display}
            {:else}
                &nbsp;
            {/if}
        </p>
    </div>
    <div>
        <button on:click={() => clearCalcul()}>C</button>
        <button on:click={() => delFromCalcul()}>DEL</button>
        <button on:click={() => addToCalcul()}>&nbsp;%&nbsp;</button>
        <button on:click={() => addToCalcul()}>&nbsp;/&nbsp;</button>
    </div>
    <div>
        <button on:click={() => addToCalcul()}>7</button>
        <button on:click={() => addToCalcul()}>8</button>
        <button on:click={() => addToCalcul()}>9</button>
        <button on:click={() => addToCalcul()}>&nbsp;*&nbsp;</button>
    </div>
    <div>
        <button on:click={() => addToCalcul()}>4</button>
        <button on:click={() => addToCalcul()}>5</button>
        <button on:click={() => addToCalcul()}>6</button>
        <button on:click={() => addToCalcul()}>&nbsp;-&nbsp;</button>
    </div>
    <div>
        <button on:click={() => addToCalcul()}>1</button>
        <button on:click={() => addToCalcul()}>2</button>
        <button on:click={() => addToCalcul()}>3</button>
        <button on:click={() => addToCalcul()}>&nbsp;+&nbsp;</button>
    </div>
    <div>
        <button on:click={() => addToCalcul()}>0</button>
        <button on:click={() => getResult()}>=</button>
    </div>
</form>

<style>
  form {
    width: 250px;
    display: flex;
    flex-direction: column;
    gap: 5px;
  }

  div {
    display: flex;
    justify-content: space-between;
    gap: 5px;
  }

  .display {
    background-color: #ccc;

    display: flex;
    flex-direction: column;

    border-radius: 5px;
    padding: 5px;
  }

  .display p {
    width: 100%;
    margin: 0;

    text-align: right;
  }

  .lastResult {
    font-size: small;
    color: #999;
  }

  button {
    width: 100%;
    padding: 0;

    border-radius: 5px;
  }
</style>