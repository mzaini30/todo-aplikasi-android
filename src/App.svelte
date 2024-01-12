<script>
  import Router from "svelte-spa-router";
  import Beranda from "./Halaman/Beranda.svelte";
  const routes = {
    "/": Beranda,
  };
</script>

<Router {routes} />
