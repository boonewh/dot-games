<script>
  import { onMount } from "svelte";

  let numDice = {
    d4: 1,
    d6: 1,
    d8: 1,
    d10: 1,
    d12: 1,
    d20: 1,
    percentile: 1,
  };

  let results = {
    d4: [],
    d6: [],
    d8: [],
    d10: [],
    d12: [],
    d20: [],
    percentile: [],
  };

  let sums = {
    d4: 0,
    d6: 0,
    d8: 0,
    d10: 0,
    d12: 0,
    d20: 0,
    percentile: 0,
  };

  let total = 0;

  function rollDice(type, numDice) {
    let result = [];
    let sum = 0;
    let i = 0;

    let diceMax = parseInt(type.slice(1));

    function rollSingleDie() {
      const roll = Math.floor(Math.random() * diceMax + 1);
      result.push(roll);
      sum += roll;
    }

    function rollNext() {
      if (i < numDice) {
        rollSingleDie();
        i++;
        results[type] = result;
        sums[type] = sum;
        updateDOM();

        setTimeout(rollNext, 250); // Quarter-second delay
      } else {
        updateTotal();
        updateDOM(); // Ensure the DOM is updated after the final roll
      }
    }

    rollNext();
  }

  function rollPercentile(numDice) {
    let result = [];
    let sum = 0;
    let i = 0;

    function roll() {
      const tens = Math.floor(Math.random() * 10) * 10;
      const ones = Math.floor(Math.random() * 10);
      const roll = tens + ones;
      result.push(roll);
      sum += roll;
    }

    function rollNext() {
      if (i < numDice) {
        roll();
        i++;
        results["percentile"] = result;
        sums["percentile"] = sum;
        updateDOM();

        setTimeout(rollNext, 250); // Quarter-second delay
      } else {
        updateTotal();
        updateDOM(); // Ensure the DOM is updated after the final roll
      }
    }

    rollNext();
  }

  function updateTotal() {
    const diceTypes = ["d4", "d6", "d8", "d10", "d12", "d20", "percentile"];
    total = 0;
    let hasValidRolls = false;

    for (const type of diceTypes) {
      const totalElement = document.getElementById(`${type}Total`);
      if (totalElement && totalElement.innerHTML !== "") {
        const totalStr = totalElement.innerHTML;
        const rollValue = parseInt(totalStr.split(": ")[1]);
        if (!isNaN(rollValue)) {
          total += rollValue;
          hasValidRolls = true;
        }
      }
    }

    document.getElementById("total").innerHTML =
      "Total of All Rolls: " + (hasValidRolls ? total : 0);
  }

  function updateDOM() {
    for (const type in results) {
      document.getElementById(`${type}Results`).innerHTML =
        `Results: ${results[type].join(", ")}`;
      document.getElementById(`${type}Total`).innerHTML =
        `Total: ${sums[type]}`;
    }
    document.getElementById("total").innerHTML = `Total of All Rolls: ${total}`;
  }

  function clearResults() {
    const diceTypes = ["d4", "d6", "d8", "d10", "d12", "d20", "percentile"];
    for (const type of diceTypes) {
      results[type] = [];
      sums[type] = 0;
    }
    total = 0;
    updateDOM();
  }

  onMount(() => {
    document.querySelectorAll(".roll-button").forEach((button) => {
      button.addEventListener("click", (event) => {
        const type = event.target.getAttribute("data-type");
        const numDice = parseInt(document.getElementById(`${type}Num`).value);
        if (type === "percentile") {
          rollPercentile(numDice);
        } else {
          rollDice(type, numDice);
        }
        updateDOM();
      });
    });

    document.getElementById("clearResults").addEventListener("click", () => {
      clearResults();
      updateDOM();
    });
  });
</script>

<svelte:head>
  <link rel="stylesheet" href="/css/main.css" />
</svelte:head>

<main>
  <h1>Dice Roller</h1>
  <div class="dice">
    <h3>Roll d4</h3>
    <p>How many would you like to roll?</p>
    <input type="number" id="d4Num" bind:value={numDice.d4} min="1" />
    <button class="roll-button" data-type="d4">Roll</button>
    <h3 id="d4Results">Results:</h3>
    <p id="d4Total"></p>
  </div>

  <div class="dice">
    <h3>Roll d6</h3>
    <p>How many would you like to roll?</p>
    <input type="number" id="d6Num" bind:value={numDice.d6} min="1" />
    <button class="roll-button" data-type="d6">Roll</button>
    <h3 id="d6Results">Results:</h3>
    <p id="d6Total"></p>
  </div>

  <div class="dice">
    <h3>Roll d8</h3>
    <p>How many would you like to roll?</p>
    <input type="number" id="d8Num" bind:value={numDice.d8} min="1" />
    <button class="roll-button" data-type="d8">Roll</button>
    <h3 id="d8Results">Results:</h3>
    <p id="d8Total"></p>
  </div>

  <div class="dice">
    <h3>Roll d10</h3>
    <p>How many would you like to roll?</p>
    <input type="number" id="d10Num" bind:value={numDice.d10} min="1" />
    <button class="roll-button" data-type="d10">Roll</button>
    <h3 id="d10Results">Results:</h3>
    <p id="d10Total"></p>
  </div>

  <div class="dice">
    <h3>Roll d12</h3>
    <p>How many would you like to roll?</p>
    <input type="number" id="d12Num" bind:value={numDice.d12} min="1" />
    <button class="roll-button" data-type="d12">Roll</button>
    <h3 id="d12Results">Results:</h3>
    <p id="d12Total"></p>
  </div>

  <div class="dice">
    <h3>Roll d20</h3>
    <p>How many would you like to roll?</p>
    <input type="number" id="d20Num" bind:value={numDice.d20} min="1" />
    <button class="roll-button" data-type="d20">Roll</button>
    <h3 id="d20Results">Results:</h3>
    <p id="d20Total"></p>
  </div>

  <div class="dice">
    <h3>Roll Percentile</h3>
    <p>How many would you like to roll?</p>
    <input
      type="number"
      id="percentileNum"
      bind:value={numDice.percentile}
      min="1"
    />
    <button class="roll-button" data-type="percentile">Roll</button>
    <h3 id="percentileResults">Results:</h3>
    <p id="percentileTotal"></p>
  </div>

  <h3 id="total">Total of All Rolls: 0</h3>

  <br />
  <button id="clearResults">Clear Results</button>
</main>

<style>
  /* Dice Roller Styles */
  input[type="number"] {
    width: 50px;
  }

  .dice {
    width: 75%;
    padding: 10px;
    border-bottom: 1px solid black;
    margin: auto;
  }
  /*
  .dicePic {
    width: 250px;
    float: right;
    border-radius: 125px;
    margin-right: 320px;
  }
*/
  #total,
  #clearResults {
    margin-left: 10%;
  }

  button {
    margin: 20px 0 30px 25px;
    width: 250px;
    height: 40px;
    transition: transform 0.3s ease;
    border-radius: 10px;
    font-family: Alkatra, Georgia, "Times New Roman", Times, serif;
    font-size: 18px;
    color: var(--text);
    background-color: var(--background);
  }
</style>
