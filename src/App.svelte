<script>
  import CoinDisplayer from "./CoinDisplayer.svelte";
  // Crypto Stats
  let stats = null;

  fetch("https://api.coinranking.com/v1/public/stats?base=USD")
    .then(res => res.json())
    .then(res => {
      stats = res.data;
      console.log(stats);
    });

  // Base coin & coins data
  let coins = null;
  let basecoin = null;
  let coinErr = false;

  fetch("https://api.coinranking.com/v1/public/coins")
    .then(response => response.json())
    .then(res => {
      coins = res.data.coins;
      basecoin = res.data.base;
    })
    .catch(exc => {
      console.log(exc);
      coinErr = true;
    });
</script>

<style>
  :global(body) {
    background-color: whitesmoke;
  }

  .title {
    font-size: 2em;
    font-weight: bold;
    text-align: center;
  }

  .coins {
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: center;
  }

  .stats {
    display: flex;
    flex-flow: row wrap;
  }
</style>

<div class="main">
  <div class="title">Cryptowatcher</div>
  <div class="stats">
    {#each stats as stat}{/each}
  </div>
  <div class="container">
    {#if coins != null}
      <div class="coins">
        {#each coins as coin}
          <CoinDisplayer {coin} basecoin={basecoin.symbol} />
        {/each}
      </div>
    {:else if !coinErr}
      Waiting response...
    {:else}Error: Couldn't fetch coins{/if}
  </div>
</div>
