<script>
  import { wrap } from "svelte-spa-router/wrap";
  import Router, {link} from "svelte-spa-router";

  import Home from "./lib/Home.svelte";
  import About from "./lib/About.svelte";
  import Learn from "./lib/Learn.svelte";
  import Policy from "./lib/Policy.svelte";

  const routes = {
    "/": wrap({ component: Home }),
    "/about": wrap({component: About}),
    "/learn": wrap({component: Learn}),
    "/policy": wrap({component: Policy})
  };
</script>

   <div class="nav-div">
   <a href="/" use:link>FlipCoin</a> <span style="color: wheat;margin:0 3px">|</span> 
    <a href="/about" use:link>About</a> <span style="color: wheat;margin:0 3px">|</span> 
    <a href="/learn" use:link>Learn</a>
   </div>
<Router {routes} />

<style>
  .nav-div {
    display: flex;
    justify-content: space-around;
    align-items: center;
    width: 200px;
    height: 32px;
    padding: 6px;
    margin: 6px;
    border-radius: 4px;
    position: fixed;
    top: 5%;
    left: 60%;
    background-color: rgb(110, 78, 141);
  }
  .nav-div a {
    color: white;
    text-decoration: none;
  }


  @media (max-width: 768px) {
    .nav-div {
      top: 2%;
      left: 15%;
      z-index: 130;
    }

  }
</style>
