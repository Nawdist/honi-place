<script lang="ts">
import ImageHolder from "./lib/ImageHolder.svelte";
import { appWindow } from '@tauri-apps/api/window'
  
</script>

<main class="container">
  <div data-tauri-drag-region class="titlebar">
    <div on:click={appWindow.minimize} class="titlebar-button" id="titlebar-minimize">
      <img
        src="https://api.iconify.design/mdi:window-minimize.svg"
        alt="minimize"
      />
    </div>
    <div on:click={appWindow.toggleMaximize} class="titlebar-button" id="titlebar-maximize">
      <img
        src="https://api.iconify.design/mdi:window-maximize.svg"
        alt="maximize"
      />
    </div>
    <div on:click={appWindow.close} class="titlebar-button" id="titlebar-close">
      <img src="https://api.iconify.design/mdi:close.svg" alt="close" />
    </div>
  </div>
  <ImageHolder/>
</main>

<style>
  
</style>