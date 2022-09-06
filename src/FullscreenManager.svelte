<script>
  import { browser } from "$app/environment";

  import { onMount, onDestroy } from "svelte";
  import { screenfull } from "./libs/screenfull.js";

  export let element;
  export let isFullscreen;
  export let isFullscreenEnabled;

  isFullscreenEnabled = screenfull.isEnabled;
  if (isFullscreenEnabled) screenfull.on("change", onChange);

  function onChange(e) {
    if (element == e.target) isFullscreen = screenfull.isFullscreen;
  }

  $: {
    if (isFullscreenEnabled)
      isFullscreen ? screenfull.request(element) : screenfull.exit();
  }

  onMount(() => {
    if (browser && window.screenfull) {
    }
  });

  onDestroy(() => {
    screenfull.off("change", onChange);
  });
</script>
