<script>
  import EmojiDisplay from "./EmojiDisplay.svelte";
  import EmojiDescription from "./EmojiDescription.svelte";
  import Button from "./Button.svelte";
  import { fade, fly } from "svelte/transition";

  let isLoaded = false;
  let currentEmoji = "😇";
  const emojis = ["🐵 ", "🐱 ", "🤡 ", "😕 "];
  let m = { x: 0, y: 0 };
  function randomizeEmoji() {
    return emojis[Math.floor(Math.random() * emojis.length)];
  }

  function handleRandomBtn() {
    currentEmoji = randomizeEmoji();
  }

  setTimeout(() => {
    isLoaded = true;
  }, 2500);

  function handleMouseMove(event) {
    m.x = event.clientX;
    m.y = event.clientY;
  }
</script>

<div class="container" on:mousemove={handleMouseMove}>
  <p>
    the mouse position {m.x} x {m.y}
  </p>
  <h1>Randomize Emoji</h1>
  <ul>
    {#each emojis as emoji}
      <li>{emoji}</li>
    {/each}
  </ul>
  {#if isLoaded === true}
    <div in:fly={{ y: 200, duration: 2000 }} out:fade>
      <EmojiDisplay {currentEmoji} />
      <EmojiDescription />
      <Button on:click={handleRandomBtn} title={"Randomize"} />
    </div>
  {:else}
    <p>Loading....</p>
  {/if}
</div>
<svelte:head>
  <link href="/terminal.min.css" rel="stylesheet" />
</svelte:head>

<style>
  div {
    margin: 2em;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
