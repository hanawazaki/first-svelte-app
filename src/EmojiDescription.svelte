<script>
  let description = "";
  $: chars = description.length;
  $: words = description.split(" ").length;
  $: console.log(`descrition {description}`);

  function handleSubmit(event) {
    console.log("Data saved");
    description = "";
  }
</script>

<div class="form-group">
  <p>
    {description}
  </p>
  <form on:submit|preventDefault={handleSubmit}>
    <textarea bind:value={description} rows="7" />
    <button>Save</button>
  </form>
  <p>Jumlah karakter : {chars}</p>
  <p>Jumlah kata : {words}</p>
</div>

<style>
  div {
    margin-top: 1em;
    margin-bottom: 1em;
  }
</style>
