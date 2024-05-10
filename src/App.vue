<template>
  <div id="app">
    <h1>Gedget Bersama</h1>
    
    <!-- Daftar produk -->
    <div class="products">
      <div v-for="product in products" :key="product.id" class="product">
        <img :src="product.image" alt="Product Image">
        <h2>{{ product.name }}</h2>
        <p>{{ product.description }}</p>
        <p>Harga: RP {{ product.price.toLocaleString('id-ID', { maximumFractionDigits: 0, minimumFractionDigits: 0 }) }}</p>
        <button @click="addToCart(product)">Add to Cart</button>
      </div>
    </div>

    <!-- Keranjang belanja -->
    <div class="cart">
      <h2>Shopping Cart</h2>
      <ul>
        <li v-for="item in cart" :key="item.id">
          {{ item.name }} - Rp{{ parseFloat(item.price).toLocaleString('id-ID') }}
          <button @click="removeFromCart(item)">Remove</button>
        </li>
      </ul>
      <p>Total: Rp{{ parseFloat(total).toLocaleString('id-ID') }}</p>
      <button @click="checkout">Checkout</button>
    </div>
  </div>


</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      products: [
        { id: 1, name: 'Kamera Sony A7 MARK III', description: 'Sony A7 Mark III adalah kamera mirrorless dengan sensor Full Frame 35 mm yang menawarkan performa tinggi dan fitur-fitur canggih', price: 79999999, image: require('@/assets/1.png')  },
        { id: 2, name: 'Lensa Samyang 35MM', description: 'Lensa Samyang 35MM adalah lensa prime dengan jarak fokus tetap 35mm yang ideal untuk fotografi potret dan street photography.', price: 57999999, image: require('@/assets/2.png')  },
        { id: 3, name: 'Memori Card 128 GB', description: 'Memori Card 128 GB adalah kartu memori berkapasitas besar yang cocok untuk menyimpan foto, video, dan file-file lainnya dengan aman dan mudah.', price: 1000000, image: require('@/assets/3.png')  },
        { id: 4, name: 'Tripot Kamera', description: 'Tripot Kamera adalah tripod yang kokoh dan stabil untuk menopang kamera Anda saat pengambilan foto atau video, memberikan stabilitas yang diperlukan untuk hasil yang jernih dan tajam.', price: 5999999, image: require('@/assets/4.png')  },
        { id: 5, name: 'Iphone 15 Pro & Promax', description: 'iPhone 15 Pro & Promax adalah smartphone terbaru dari Apple yang dilengkapi dengan fitur-fitur canggih dan kamera berkualitas tinggi untuk pengalaman pengambilan foto dan video yang luar biasa.', price: 22999999, image: require('@/assets/5.png')  },
        { id: 6, name: 'Macbook Pro 13 Inci', description: 'MacBook Pro 13 Inci adalah laptop kelas atas dari Apple yang menawarkan performa tinggi dan desain elegan, cocok untuk kebutuhan profesional dan kreatif Anda', price: 19999999, image: require('@/assets/6.png')  },
        
      ],
      cart: []
    };
  },
  computed: {
    total() {
      return this.cart.reduce((acc, item) => acc + item.price, 0);
    }
  },
  methods: {
    addToCart(product) {
      this.cart.push(product);
    },
    removeFromCart(item) {
      const index = this.cart.indexOf(item);
      if (index !== -1) {
        this.cart.splice(index, 1);
      }
    },
    checkout() {
      alert('Thank you for your purchase!');
      this.cart = [];
    }
  }
};
</script>

<style scoped>
/* General styles */
body {
  font-family: Georgia, 'Times New Roman', Times, serif;
  margin: 0;
  padding: 0;
  background-color: #f2f2f2;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}

h1 {
  text-align: center;
  color: #333;
  margin-top: 0px;
  margin-bottom: 30px;
  border: 2px solid #e65c00;
  border-radius: 10px;
  padding: 10px 20px; /* Tambahkan padding agar tulisan tidak terlalu dekat dengan border */
  background-color: #f8f8f8; /* Warna latar belakang */
  border-color: #ff6600; /* Warna border */

}




/* Product styles */
.products {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

.product {
  background-color: #fff;
  border-radius: 10px;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
  padding: 20px;
  margin-bottom: 20px;
  width: calc(33.33% - 20px);
  box-sizing: border-box;
  transition: transform 0.3s ease;
}

.product:hover {
  transform: translateY(-5px);
}

.product img {
  width: 100%;
  max-width: 150px;
  height: auto;
  border-radius: 10px;
  margin-bottom: 10px;
}

.product h2 {
  font-size: 20px;
  margin-top: 15px;
  margin-bottom: 10px;
  color: #333;
}

.product p {
  color: #666;
  margin-bottom: 10px;
  overflow: hidden; 
  text-overflow: ellipsis; 
}

.product button {
  background-color: #ff6600;
  color: #fff;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.product button:hover {
  background-color: #e65c00;
}

/* Media query for mobile */
@media screen and (max-width: 768px) {
  .products {
    flex-wrap: wrap;
    justify-content: space-around;
  }

  .product {
    width: calc(50% - 20px);
    margin-bottom: 20px;
  }
}

/* Cart styles */
.cart {
  background-color: #fff;
  border-radius: 10px;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
  padding: 20px;
  margin-top: 30px;
}

.cart h2 {
  font-size: 24px;
  color: #333;
  margin-bottom: 20px;
}

.cart ul {
  padding: 0;
  list-style-type: none;
}

.cart li {
  font-size: 18px;
  margin-bottom: 10px;
}

.cart p {
  font-size: 20px;
  margin-top: 20px;
  color: #333;
}

.cart button {
  background-color: #ff6600;
  color: #fff;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.cart button:hover {
  background-color: #e65c00;
}

</style>


