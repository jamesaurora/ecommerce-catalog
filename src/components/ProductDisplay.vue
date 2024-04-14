<template>
  <div class="background">
    <div class="content">
      <div class="container">
        <div class="box">
          <div class="group-4">
            <div class="women-jacket-1">
            <img :src="product.image" :alt="product.title" style="max-width: 100%; max-height: 100%;">
          </div>
            <div class="container-2">
              <div class="container">
                <div class="jaket-wanita">
                  {{ product.title }}
                </div>
                <div class="group-3">
                  <div v-for="i in Math.ceil(product.rating.rate)" :key="i" :class="'ellipse-' + i"></div>
                </div>
                <div class="kategori">
                  {{ product.category }}
                </div>
                <div class="rating">
                  {{ product.rating.rate }}/5
                </div>
              </div>
              <div class="deskripsi-barang">
                {{ product.description }}
              </div>
              <div class="harga">
                {{ product.price | formatCurrency }}
              </div>
              <div class="container-1">
                <div class="group-1">
                  <span class="buy-now">Buy now</span>
                </div>
                <div class="group-2">
                  <button class="next-product" @click="nextProduct" :disabled="loading">Next product</button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>   
    </div>
    <div v-if="loading" class="loader"></div> <!-- Loader element -->
  </div>
</template>

<script>
export default {
  name: 'ProductDisplay',
  data() {
    return {
      product: {}, // Variabel untuk menyimpan data produk
      currentIndex: 1, // Variabel untuk melacak indeks produk yang ditampilkan
      loading: false // Variabel untuk menandai apakah data sedang dimuat atau tidak
    };
  },
  created() {
    this.fetchProduct(); // Memanggil method fetchProduct saat komponen dibuat
  },
  methods: {
    async fetchProduct() {
      try {
        this.loading = true; // Tandai bahwa data sedang dimuat
        const response = await fetch(`https://fakestoreapi.com/products/${this.currentIndex}`);
        const data = await response.json();
        this.product = data; // Simpan data produk yang diterima ke dalam variabel product
      } catch (error) {
        console.error('Error fetching product:', error);
      } finally {
        this.loading = false; // Hentikan penandaan bahwa data sedang dimuat
      }
    },
    nextProduct() {
      this.currentIndex++; // Increment indeks produk
      if (this.currentIndex > 20) {
        this.currentIndex = 1; // Jika indeks mencapai 20, atur kembali ke 1
      }
      this.fetchProduct(); // Panggil method fetchProduct untuk mendapatkan produk berikutnya
    }
  }
};
</script>

<style>
@import url('/src/assets/style/page.css');

.loader {
  border: 8px solid #f3f3f3; /* Warna latar belakang loader */
  border-top: 8px solid #3498db; /* Warna garis atas loader */
  border-radius: 50%;
  width: 50px;
  height: 50px;
  animation: spin 1s linear infinite; /* Animasi putaran loader */
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}
</style>
