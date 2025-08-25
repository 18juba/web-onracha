<script>
  import "../app.css";
  import favicon from "$lib/assets/favicon.svg";
  import "@fontsource/source-code-pro";
  // import bg from "../lib/assets/img/bg.png";

  let { children } = $props();
</script>

<svelte:head>
  <link rel="icon" href={favicon} />
</svelte:head>

<main class="antialiased font1 relative min-h-screen bg-gradient-to-br from-slate-950 via-emerald-950 to-slate-950">
  <!-- {#if bg}
    <img src={bg} alt="Fundo" class="fixed h-full w-full object-cover -z-50" />
  {/if} -->

  {@render children?.()}
</main>
