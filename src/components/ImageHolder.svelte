<script lang="ts">
  import { onMount } from "svelte";

  import { Alert, Spinner } from "sveltestrap";
  $: loading = false;
  let error: string = null;
  $: currentCat = {
    src: "/loading.gif",
    width: 400,
    height: 400,
    gif: false,
  };
  async function getCat() {
    let gif = Math.random() < 0.3 ? "/gif" : "";
    console.log("clickeds");
    // let result: Response;
    try {
      loading = true;
      currentCat = {
        src: "/loading.gif",
        width: 400,
        height: 400,
        gif: false,
      };
      let p = fetch("https://cataas.com/cat" + gif, {
        method: "GET",
        cache: "no-cache",
      });
      let result = await p;
      let res_blob = await result.blob();
      // throw new SyntaxError("trolled")
      let img = new Image();
      img.src = window.URL.createObjectURL(res_blob);
      img.onload = () => {
        loading = false;
        let { width: _width, height: _height, src } = img;
        let ratio = _width / _height;
        let height = 400;
        let width = height * ratio;
        currentCat = { width, height, src, gif: !!gif };
      };
    } catch (err) {
      currentCat = {
        src: "/loading.gif",
        width: 400,
        height: 400,
        gif: false,
      };
      error =
      "Ran into an error while requesting from cat source. Using fallback source..";
      loading = true;
      let result = await fetch("https://api.thecatapi.com/v1/images/search", {
        method: "GET",
        cache: "no-cache",
      });
      let res = await result.json();
      let { width: _width, height: _height, url: src } = res[0];
      let ratio = _width / _height;
      let height = 400;
      let width = height * ratio;
      currentCat = { width, height, src, gif: !!gif };
      loading = false;
    }
  }
</script>

<div class="cat-container">
  <img {...currentCat} alt="kitty!" />
  <button class="btn-purple" on:click={getCat}>Get kitty</button>
  {#if loading}
    <Spinner class="spin" color="warning" />
  {/if}
  {#if error}
    <Alert size={2} color="danger">
      <h4>Kiggy Error</h4>
      <p>{error}</p>
    </Alert>
  {/if}
</div>

<style>
  .cat-container {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .cat-container .btn-purple {
    margin-top: 10px;
    color: black;
    border: 1px black solid;
    border-radius: 5%;
    background-color: rgb(250, 129, 0);
    font-size: 1.5rem;
    padding: 7px;
    font-weight: bold;
    transition: 0.3s;
  }
  .cat-container .btn-purple:hover {
    background-color: rgb(255, 155, 49);
    box-shadow: 2px 2px 10px rgb(251, 243, 220)
  }
</style>
