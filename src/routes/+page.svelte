<script>
    let lastResult = "";
    let display = "";

    function isDigit(x) {
        return "0" <= x && x <= "9";
    }

    function isOperator(x) {
        return x === "+" || x === "-" || x === "*" || x === "/" || x === "%";
    }

    function addToCalcul(x) {
        if (display.length > 0) {
            if (isDigit(x)) {
                if (isOperator(display.slice(-1))) {
                    display += " ";
                }
            } else if (isOperator(x)) {
                if (display.slice(-1) === "." || isOperator(display.slice(-1))) {
                    display = display.slice(0, -1);
                } else if (isDigit(display.slice(-1))) {
                    display += " ";
                }
            }
        } else if (isOperator(x)) {
            if (x !== "-" && x !== "+") return;
        }
        display += x;
    }

    function clearCalcul() {
        display = "";
    }

    function delFromCalcul() {
        display = display.slice(0, -1);
        if (display.length > 0 && display.slice(-1) === " ") {
            display = display.slice(0, -1);
        }
    }

    function getResult() {
        if (display.length === 0) return;
        lastResult = eval(display);
        if (lastResult === undefined) {
            lastResult = "0";
        }
        display = "";
    }
</script>

<form>
    <div class="top">
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
    </div>
    <div class="bottom">
        <div class="btn-line">
            <button on:click={() => clearCalcul()}>C</button>
            <button on:click={() => delFromCalcul()}>DEL</button>
            <button on:click={() => addToCalcul("%")}>%</button>
            <button on:click={() => addToCalcul("/")}>/</button>
        </div>
        <div class="btn-line">
            <button on:click={() => addToCalcul("7")}>7</button>
            <button on:click={() => addToCalcul("8")}>8</button>
            <button on:click={() => addToCalcul("9")}>9</button>
            <button on:click={() => addToCalcul("*")}>*</button>
        </div>
        <div class="btn-line">
            <button on:click={() => addToCalcul("4")}>4</button>
            <button on:click={() => addToCalcul("5")}>5</button>
            <button on:click={() => addToCalcul("6")}>6</button>
            <button on:click={() => addToCalcul("-")}>-</button>
        </div>
        <div class="btn-line">
            <button on:click={() => addToCalcul("1")}>1</button>
            <button on:click={() => addToCalcul("2")}>2</button>
            <button on:click={() => addToCalcul("3")}>3</button>
            <button on:click={() => addToCalcul("+")}>+</button>
        </div>
        <div class="btn-line">
            <button on:click={() => addToCalcul("0")}>0</button>
            <button on:click={() => getResult()}>=</button>
        </div>
    </div>
</form>

<style>
  form {
    width: 250px;

    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);

    background-color: #22262b;

    border-radius: 15px;
  }

  .top {
    padding: 15px;
  }

  .bottom {
    padding: 15px;

    display: flex;
    flex-direction: column;
    gap: 5px;

    background-color: #2a2c34;
    border-radius: 15px;
  }

  .btn-line {
    height: 50px;

    display: flex;
    justify-content: space-between;
    gap: 5px;
  }

  .display {
    display: flex;
    flex-direction: column;

    color: #fff;

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
    color: #888888;
  }

  button {
    width: 100%;
    padding: 0;

    background-color: #22262b;
    color: #fff;

    border-radius: 5px;
    border: none;
  }
</style>
