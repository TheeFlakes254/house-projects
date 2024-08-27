<script>
  // Import necessary components
  import Header from '../components/Header.svelte';
  import Footer from '../components/Footer.svelte';
  import HouseListings from './houses/HouseListings.svelte';
</script>

<main>
  <Header />
  <HouseListings />
  <Footer />
</main>

<style>
  main {
    display: grid;
    grid-template-rows: auto 1fr auto;
    min-height: 100vh;
  }
</style>