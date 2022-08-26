<script lang="ts">
  $: currentCat = {src: "", width: 0, height: 0};
  async function getCat() {
    // let result = await fetch("https://api.thecatapi.com/v1/images/search");
    // let current = await result.clone().json();
    // currentCat = current[0].url;
    let result = await fetch("https://cataas.com/cat", {
      method: "GET",
      cache: "no-cache"
    });
    let res_blob = await result.blob();
    let img = new Image()
    img.src = window.URL.createObjectURL(res_blob);
    img.onload = () => {
      let {width: _width, height: _height, src} = img
      let ratio = _width / _height
      let height = 500;
      let width = height * ratio;
      currentCat = {width, height, src}
      console.log("clickeds");
    }
  }
</script>

<div>
  <img {...currentCat} alt="kitty!" />
  <button on:click={getCat}>Get kitty</button>
</div>
