<template>
    <div class="background">
      <div class="content">
        <div class="container">
          <div class="box">
            <div class="sad-face">
              😞
            </div>
            <div class="message">
              <p>This product is unavailable to show.</p>
              <p>Next product</p>
            </div>
            <button class="next-product" @click="nextProduct">Next product</button>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'ProductnotAvailable',
    data() {
      return {
        lastDisplayedIndex: 0 // Indeks produk terakhir yang ditampilkan sebelumnya
      };
    },
    methods: {
      nextProduct() {
        // Increment indeks produk terakhir
        this.lastDisplayedIndex++;
        // Jika indeks mencapai 20, atur kembali ke 1
        if (this.lastDisplayedIndex > 20) {
          this.lastDisplayedIndex = 1;
        }
        // Panggil method fetchProduct untuk mendapatkan produk berikutnya dari indeks yang baru
        this.fetchProduct();
      },
      async fetchProduct() {
        try {
          this.loading = true; // Tandai bahwa data sedang dimuat
          const response = await fetch(`https://fakestoreapi.com/products/${this.lastDisplayedIndex}`);
          const data = await response.json();
          // Tampilkan produk yang berhasil diambil
          console.log('Next product:', data);
          // Menggunakan fungsi callback untuk mengirimkan data produk ke komponen induk
          this.$emit('product-fetched', data);
        } catch (error) {
          console.error('Error fetching product:', error);
        } finally {
          this.loading = false; // Hentikan penandaan bahwa data sedang dimuat
        }
      }
    }
  };
  </script>
  

<style>
@import url('/src/assets/style/page3.css');
</style>