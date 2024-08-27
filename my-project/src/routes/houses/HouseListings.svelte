<script>
  // Import necessary modules and components
  import HouseCard from '$components/HouseCard.svelte';

  // Fetch house listings from the backend API
  let houseListings = [];
  async function fetchHouseListings() {
    const response = await fetch('/api/houses');
    houseListings = await response.json();
  }
  fetchHouseListings();
</script>

<main class="container mx-auto py-8">
  <h1 class="text-3xl font-bold mb-4">House Listings</h1>
  <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-4">
    {#each houseListings as house}
      <HouseCard {house} />
    {/each}
  </div>
</main>