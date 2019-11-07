<script>
  import CoinDisplayer from "./CoinDisplayer.svelte";

  let minutes = x => x * 60000;

  // Crypto Stats
  let stats = null;
  async function getStatsData() {
  fetch("https://api.coinranking.com/v1/public/stats?base=USD")
    .then(res => res.json())
    .then(res => {
      stats = res.data;
      console.log(stats);
    });
  }
  const statsInterval = setInterval(getStatsData, 5);

  // Base coin & coins data
  let coins = null;
  let basecoin = null;
  let coinErr = false;
  async function getCoinsData() {
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
  }
  const coinsInterval = setInterval(getCoinsData, 5);
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
