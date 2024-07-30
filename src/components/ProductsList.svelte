<script>
  import { onMount } from 'svelte';

  let products = [];
  let loading = true;
  let error = null;

  async function getProducts() {
  try {
    let response = await fetch('https://fakestoreapi.com/products');
    if (!response.ok) {
      throw new error("Failed to fetch products");
    }
    products = await response.json();
  } catch (err) {
    error = err.message;
  } finally {
    loading = false;
  }
}

onMount(() => {
  getProducts();
});
</script>
<style></style>
<main>
    <p>whatever</p>
</main>