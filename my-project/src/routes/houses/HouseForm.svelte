<script>
  // Import necessary modules and components
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();

  // House form state
  let title = '';
  let description = '';
  let price = 0;
  let bedrooms = 0;
  let bathrooms = 0;
  let sqft = 0;
  let address = '';
  let images = [];

  // Handle form submission
  async function handleSubmit() {
    const houseData = {
      title,
      description,
      price,
      bedrooms,
      bathrooms,
      sqft,
      address,
      images
    };

    const response = await fetch('/api/houses', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify(houseData)
    });

    if (response.ok) {
      dispatch('house-created', houseData);
      // Reset form fields
      title = '';
      description = '';
      price = 0;
      bedrooms = 0;
      bathrooms = 0;
      sqft = 0;
      address = '';
      images = [];
    }
  }

  // Handle image upload
  function handleImageUpload(event) {
    images = [...event.target.files];
  }
</script>

<main class="container mx-auto py-8">
  <h1 class="text-3xl font-bold mb-4">Add a New House Listing</h1>
  <form on:submit|preventDefault={handleSubmit} class="space-y-4">
    <div>
      <label for="title" class="block font-medium">Title</label>
      <input type="text" id="title" bind:value={title} class="border rounded-md px-3 py-2 w-full" required>
    </div>
    <div>
      <label for="description" class="block font-medium">Description</label>
      <textarea id="description" bind:value={description} class="border rounded-md px-3 py-2 w-full" required></textarea>
    </div>
    <div class="grid grid-cols-3 gap-4">
      <div>
        <label for="price" class="block font-medium">Price</label>
        <input type="number" id="price" bind:value={price} class="border rounded-md px-3 py-2 w-full" required>
      </div>
      <div>
        <label for="bedrooms" class="block font-medium">Bedrooms</label>
        <input type="number" id="bedrooms" bind:value={bedrooms} class="border rounded-md px-3 py-2 w-full" required>
      </div>
      <div>
        <label for="bathrooms" class="block font-medium">Bathrooms</label>
        <input type="number" id="bathrooms" bind:value={bathrooms} class="border rounded-md px-3 py-2 w-full" required>
      </div>
    </div>
    <div class="grid grid-cols-2 gap-4">
      <div>
        <label for="sqft" class="block font-medium">Square Feet</label>
        <input type="number" id="sqft" bind:value={sqft} class="border rounded-md px-3 py-2 w-full" required>
      </div>
      <div>
        <label for="address" class="block font-medium">Address</label>
        <input type="text" id="address" bind:value={address} class="border rounded-md px-3 py-2 w-full" required>
      </div>
    </div>
    <div>
      <label for="images" class="block font-medium">Images</label>
      <input type="file" id="images" multiple on:change={handleImageUpload} class="border rounded-md px-3 py-2 w-full" required>
    </div>
    <button type="submit" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
      Submit
    </button>
  </form>
</main>