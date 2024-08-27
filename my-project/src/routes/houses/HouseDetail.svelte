<script>
  // Import necessary modules and components
  import ImageGallery from '$components/ImageGallery.svelte';

  // Fetch house details from the backend API
  export let id;
  let house = {};
  async function fetchHouseDetails() {
    const response = await fetch(`/api/houses/${id}`);
    house = await response.json();
  }
  fetchHouseDetails();
</script>

<main class="container mx-auto py-8">
  <h1 class="text-3xl font-bold mb-4">{house.title}</h1>
  <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
    <div>
      <ImageGallery images={house.images} />
    </div>
    <div>
      <p>{house.description}</p>
      <p>Price: ${house.price}</p>
      <p>Bedrooms: {house.bedrooms}</p>
      <p>Bathrooms: {house.bathrooms}</p>
      <p>Square Feet: {house.sqft}</p>
      <p>Address: {house.address}</p>
    </div>
  </div>
</main>