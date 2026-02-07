<script>
  import Router from "svelte-spa-router";
  import Login from "./routes/login.svelte";
  import Dashboard from "./routes/dashboard.svelte";
  
  const routes = {
    "/": Login,
    "/dashboard": Dashboard
  };
</script>

<main>
  <Router {routes} />
</main>

<style>
  main {
    padding: 2em;
    font-family: 'Arial', sans-serif;
  }

  h1 {
    color: #FF6B00;
  }
</style>
