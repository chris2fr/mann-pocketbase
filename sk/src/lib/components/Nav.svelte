<script lang="ts">
  import { base } from "$app/paths";
  import { page } from "$app/stores";
  const links = [
    ["/", "Home"],
    ["/consultations/", "Consultations"],
    // ["/hello/", "Hello"],
  ];
</script>

<nav>
  {#each links as [path, label]}
    {@const active = $page.url.pathname == path}
    <a href={`${base}${path}`} class:active>{label}</a>
  {/each}
</nav>

<style lang="scss">
  nav {
    a {
      padding: 0.5em 1em;
      margin: 0;
      background: var(--background-alt);
      border-bottom: solid var(--background);
      &.active {
        background: var(--background);
        font-weight: bold;
        border-bottom: solid var(--links);
      }
    }
  }
</style>
