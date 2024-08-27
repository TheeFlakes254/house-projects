<script>
  // Import necessary modules and components
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();

  // Login form state
  let email = '';
  let password = '';

  // Handle form submission
  async function handleLogin() {
    const userData = {
      email,
      password
    };

    const response = await fetch('/api/login', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify(userData)
    });

    if (response.ok) {
      dispatch('login-success', userData);
      // Reset form fields
      email = '';
      password = '';
    }
  }
</script>

<main class="container mx-auto py-8">
  <h1 class="text-3xl font-bold mb-4">Login</h1>
  <form on:submit|preventDefault={handleLogin} class="space-y-4">
    <div>
      <label for="email" class="block font-medium">Email</label>
      <input type="email" id="email" bind:value={email} class="border rounded-md px-3 py-2 w-full" required>
    </div>
    <div>
      <label for="password" class="block font-medium">Password</label>
      <input type="password" id="password" bind:value={password} class="border rounded-md px-3 py-2 w-full" required>
    </div>
    <button type="submit" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
      Login
    </button>
  </form>
</main>