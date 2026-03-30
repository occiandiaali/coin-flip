<script>
  import { wrap } from "svelte-spa-router/wrap";
  import Router from "svelte-spa-router";

  import Home from "./lib/Home.svelte";
  import About from "./lib/About.svelte";

  const routes = {
    "/": wrap({ component: Home }),
    "/about": wrap({component: About})
  };
</script>

<Router {routes} />
