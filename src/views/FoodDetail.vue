<template>
  <div class="food-detail">
    <Navbar />
    <div class="container mt-4">
      <!-- BreadCrumb -->
      <div class="row">
        <div class="col">
          <nav
            class="rounded-2 py-2 px-3 bg-secondary-subtle"
            style="--bs-breadcrumb-divider: '/'"
            aria-label="breadcrumb"
          >
            <ol class="breadcrumb m-auto">
              <li class="breadcrumb-item">
                <router-link class="text-dark text-decoration-none" to="/"
                  >Home</router-link
                >
              </li>
              <li class="breadcrumb-item">
                <router-link class="text-dark text-decoration-none" to="/foods"
                  >Foods</router-link
                >
              </li>
              <li class="breadcrumb-item active" aria-current="page">
                Food Detail
              </li>
            </ol>
          </nav>
        </div>
      </div>

      <!-- FoodDetail -->
      <div class="row mt-4">
        <div class="col-12 col-md-6">
          <img
            :src="'../assets/images/' + product.gambar"
            class="img-fluid shadow"
          />
        </div>
        <div class="col-12 col-md-6">
          <h2>
            <strong>{{ product.nama }}</strong>
          </h2>
          <hr />
          <h4>
            Harga : <strong>Rp. {{ product.harga }}</strong>
          </h4>
          <form class="col" v-on:submit.prevent>
            <div class="form-group mt-3 mb-3">
              <label for="jumlah_pemesanan">Jumlah Pesan</label>
              <input
                type="number"
                class="form-control"
                v-model="pesan.jumlah_pemesanan"
              />
            </div>
            <div class="form-group mt-3 mb-3">
              <label for="kerangan">Keterangan</label>
              <textarea
                class="form-control"
                placeholder="Keterangan spt: Pedas, Nasi Setengah..."
                v-model="pesan.keterangan"
              >
              </textarea>
            </div>
            <button type="submit" class="btn btn-success" @click="pemesanan">
              <b-icon-cart></b-icon-cart>Pesan
            </button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import axios from "axios";

export default {
  name: "FoodDetail",
  components: {
    Navbar,
  },

  data() {
    return {
      product: {},
      pesan: {},
    };
  },

  methods: {
    setProduct(data) {
      this.product = data;
    },
    pemesanan() {
      this.pesan.products = this.product;
      if (this.pesan.jumlah_pemesanan) {
        axios
          .post("http://localhost:3000/keranjangs", this.pesan)
          .then(() => {
            this.$router.push({ path: "/keranjang" });
            this.$swal({
              title: "Pesanan Masuk Keranjang",
              icon: "success",
              timer: 3000,
              toast: true,
              position: "top-end",
              showConfirmButton: false,
              timerProgressBar: true,
            });
          })
          .catch((err) => console.log(err));
      } else {
        this.$swal({
          title: "Tolong Isi Jumlah Pesanan",
          icon: "error",
          timer: 3000,
          toast: true,
          position: "top-end",
          showConfirmButton: false,
          timerProgressBar: true,
        });
      }
    },
  },

  mounted() {
    axios
      .get("http://localhost:3000/products/" + this.$route.params.id)
      .then((response) => this.setProduct(response.data))
      .catch((error) => console.log(error));
  },
};
</script>

<style>
</style>