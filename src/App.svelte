<script lang="ts">
  import { getContext } from "svelte";
  import { Link, Router, Route } from "svelte-navigator";
  import { appWindow } from "@tauri-apps/api/window";
  import {
    Button,
    Accordion,
    AccordionItem,
    AccordionHeader,
    Icon,
    Offcanvas,
    Styles,
    ListGroup,
    ListGroupItem,
  } from "sveltestrap";
  // import {Icon, Styles} from "sveltestrap";
  import ArtPortal from "./pages/ArtPortal.svelte";
  import GenshinPortal from "./pages/GenshinPortal.svelte";
  import KittyPortal from "./pages/KittyPortal.svelte";

  let open = false;
  let toggle = () => (open = !open);
</script>

<Styles />
<Router>
  <div data-tauri-drag-region class="titlebar">
    <div class="titlebar-title">
      <img width="18" height="18" src="/loading.gif" alt=""/>
      <p>Honi's Palace</p>
    </div>
    <div
      on:click={appWindow.minimize}
      class="titlebar-button"
      id="titlebar-minimize"
    >
      <img
        src="https://api.iconify.design/mdi:window-minimize.svg"
        alt="minimize"
      />
    </div>
    <div
      on:click={appWindow.toggleMaximize}
      class="titlebar-button"
      id="titlebar-maximize"
    >
      <img
        src="https://api.iconify.design/mdi:window-maximize.svg"
        alt="maximize"
      />
    </div>
    <div on:click={appWindow.close} class="titlebar-button" id="titlebar-close">
      <img src="https://api.iconify.design/mdi:close.svg" alt="close" />
    </div>
  </div>
  <Offcanvas
    color="dark"
    isOpen={open}
    {toggle}
    header="🧡 Honi's Palace 🧡"
    placement="start"
  >
    <ListGroup>
      <Link to="/"
        ><ListGroupItem
          ><img src="/Black_paw.svg" width="20" height="20" alt="paw" /> Kitty Time!</ListGroupItem
        ></Link
      >
      <Link to="/genshin"
        ><ListGroupItem
          ><img src="/genshinlogo.png" width="20" height="20" alt="paw" /> Genshin
          Stuff</ListGroupItem
        ></Link
      >
      <ListGroupItem><Icon name="pencil-fill" /> Art Section</ListGroupItem>
      <ListGroupItem
        ><img src="/cooking.svg" width="20" height="20" alt="paw" /> Cooking Section</ListGroupItem
      >
      <ListGroupItem
        ><img src="/dice.svg" width="20" height="20" alt="paw" /> Minigames</ListGroupItem
      >
      <ListGroupItem><Icon name="question" /> Some Other Junk</ListGroupItem>
    </ListGroup>
    <ListGroup style="position: absolute; top: 80vh !important;">
      <Link to="/"
        ><ListGroupItem
          ><img width="30" height="30" src="/settings.svg" alt="settings" /> Settings</ListGroupItem
        ></Link
      >
      <a href="/*" on:click|preventDefault={appWindow.close}>
        <ListGroupItem>
          <img width="30" height="30" src="/logout.svg" alt="quit app" /> Quit</ListGroupItem
        >
      </a>
    </ListGroup>
  </Offcanvas>
  <a on:click|preventDefault={toggle} class="offcanvas-trigger" href="*"
    ><Icon name="menu-button-wide" /></a
  >
  <main class="container">
    <main>
      <Route path="/" component={KittyPortal} />
      <Route path="/genshin" component={GenshinPortal}>
        <!-- <Icon name="close" /> -->
      </Route>
      <Route path="/art" component={ArtPortal} />
    </main>
  </main></Router
>

<style>
  .offcanvas-trigger {
    font-size: 2rem;
    position: fixed;
    left: 10px;
    color: white;
    transition: 0.3s;
  }
  .offcanvas-trigger:hover {
    filter: brightness(50%);
  }
</style>
