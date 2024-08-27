<script>
  // Import necessary modules and components
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();

  // Registration form state
  let name = '';
  let email = '';
  let password = '';

  // Handle form submission
  async function handleRegister() {
    const userData = {
      name,
      email,
      password
    };

    const response = await fetch('/api/register', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify(userData)
    });

    if (response.ok) {
      dispatch('registration-success', userData);
      // Reset form fields
      name = '';
      email = '';
      password = '';
    }
  }
</script>

<main class="container mx-auto py-8">
  <h1 class="text-3xl font-bold mb-4">Register</h1>
  <form on:submit|preventDefault={handleRegister} class="space-y-4">
    <div>
      <label for="name" class="block font-medium">Name</label>
      <input type="text" id="name" bind:value={name} class="border rounded-md px-3 py-2 w-full" required>
    </div>
    <div>
      <label for="email" class="block font-medium">Email</label>
      <input type="email" id="email" bind:value={email} class="border rounded-md px-3 py-2 w-full" required>
    </div>
    <div>
      <label for="password" class="block font-medium">Password</label>
      <input type="password" id="password" bind:value={password} class="border rounded-md px-3 py-2 w-full" required>
    </div>
    <button type="submit" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
      Register
    </button>
  </form>
</main>