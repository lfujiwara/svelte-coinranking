<script>
  // DOCS
  /*
    coin.name
    coin.value
    basecoin (name)
*/
  export let coin;
  export let basecoin;
</script>

<style>
  .main {
    border: 1px solid black;
    padding: 1em;
    width: 250px;
    height: 150px;
    margin: 5px;
    border-radius: 5px;
  }
</style>

<div class="main">
  <h2>{coin.name} - {basecoin}</h2>
  <h3>{coin.price} {basecoin}</h3>
</div>
