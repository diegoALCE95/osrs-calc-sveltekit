<script>
  let valueOne = $state(0);
  let valueTwo = $state(0);
  let valueSale = $state(0);

  let cost = $state(0);
  let saleAfterTax = $state(0);
  let profit = $state(0);
  let result = $state('');
</script>

<div class="container mx-auto grid place-items-center h-screen max-w-4xl">
  <div class="grid grid-cols-2 p-5 gap-x-60">
    <div class="flex flex-col gap-5">
      <div class="form-control">
        <label for="valueOne">Value Item #1</label>
        <input type="number" id="valueOne" bind:value={valueOne} class="input input-lg bg-base-200" />
      </div>
      
      <div class="form-control">
        <label for="valueTwo">Value Item #2</label>
        <input type="number" id="valueTwo" bind:value={valueTwo} class="input input-lg bg-base-200" />
      </div>

      <div class="form-control">
        <label for="valueSale">G.E Sale Value Item</label>
        <input type="number" id="valueSale" bind:value={valueSale} class="input input-lg bg-base-200" />
      </div>

      <button
        class="btn btn-primary"
        onclick={() => {
          // total production cost
          cost = Number(valueOne) + Number(valueTwo);

          // GE tax (2% of sale value, capped at 5m, rounded down)
          let rawTax = Math.ceil(Number(valueSale) * 0.02);
          let tax = Math.min(rawTax, 5_000_000);

          // sale value after tax
          saleAfterTax = Number(valueSale) - tax;

          // profit or loss
          profit = saleAfterTax - cost;

          if (Number(valueOne) > 0 || Number(valueTwo) > 0) {
            if (Number(valueSale) > 0) {
              result =
                profit >= 0
                  ? `Profit: ${profit} GP`
                  : `Loss: ${Math.abs(profit)} GP`;
            } else {
              result = '';
            }
          } else {
            result = 'Please use the first field at least.';
          }
        }}
      >
        Calculate
      </button>

      <p class="text-xs mt-5">Note: Always add the G.E Actively traded price values.</p>
    </div>

    <div>
      <h2 class="text-2xl font-bold mb-5">Result:</h2>
      {#if result !== ''}
        <!-- <p>Value one: {valueOne}</p>
        <p>Value two: {valueTwo}</p>
        <p>G.E Sale price: {valueSale}</p>
        <p>Production cost: {sumItemValues}</p>
        <p>Production cost ({sumItemValues}) - 2%: {itemValuesMinusGeTax} GP</p>
        <p>Final price: {sumItemValuesUpdated}</p> -->
        <p class="text-2xl mt-5">{result}</p>
      {/if}
    </div>
  </div>
</div>
