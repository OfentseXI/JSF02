<script>
    function shoppingCart() {
        return {
          originalProducts: [], // Store original order of products
          categories: [],
          filteredProducts: [],
          selectedCategory: "",
          sorting: 'default', // Default sorting
          selectedProduct: {},

          async init() {
            await this.fetchCategories();
            await this.fetchProducts();
            this.loading = false;
          },

          async fetchCategories() {
            try {
              const response = await fetch("https://fakestoreapi.com/products/categories");
              this.categories = await response.json();
            } catch (error) {
              console.error("Error fetching categories:", error);
            }
          },

          async fetchProducts() {
            try {
              const response = await fetch("https://fakestoreapi.com/products");
              this.products = await response.json();
              this.originalProducts = [...this.products]; // Store original products
              this.filteredProducts = this.products;
            } catch (error) {
              console.error("Error fetching products:", error);
            }
          },

          filterProducts() {
            if (this.selectedCategory) {
              this.filteredProducts = this.products.filter(product => product.category === this.selectedCategory);
            } else {
              this.filteredProducts = this.products;
            }
            this.sortProducts();
          },

          handleSort() {
            this.sortProducts();
          },

          sortProducts() {
            if (this.sorting === "low") {
              this.filteredProducts.sort((a, b) => a.price - b.price);
            } else if (this.sorting === "high") {
              this.filteredProducts.sort((a, b) => b.price - a.price);
            } else {
              this.filteredProducts = [...this.originalProducts]; // Reset to original order
              if (this.selectedCategory) {
                this.filteredProducts = this.filteredProducts.filter(product => product.category === this.selectedCategory);
              }
            }
          },

          resetFilters() {
            this.selectedCategory = "";
            this.sorting = 'default';
            this.filteredProducts = [...this.originalProducts];
          },

          toggleNavbar() {
            this.navbarOpen = !this.navbarOpen;
          },
        };
      }
</script>

<style></style>
<main>
    <p>what!</p>
</main>