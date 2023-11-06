<template>
  <div class="keranjang">
    <Navbar :updateKeranjangs="keranjangs" />
    <div class="container">
      <!-- BreadCrumb -->
      <div class="row mt-4">
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
                Keranjang
              </li>
            </ol>
          </nav>
        </div>
      </div>

      <!-- table keranjang -->
      <div class="row mt-4">
        <div class="col">
          <h2>Keranjang <strong>Saya</strong></h2>
          <div class="table-responsive mt-3">
            <table class="table">
              <thead>
                <tr>
                  <th class="text-center" scope="col">#</th>
                  <th class="text-center" scope="col">Foto</th>
                  <th class="text-center" scope="col">Makanan</th>
                  <th class="text-center" scope="col">Keterangan</th>
                  <th class="text-center" scope="col">Jumlah</th>
                  <th class="text-center" scope="col">Harga</th>
                  <th class="text-center" scope="col">Total Harga</th>
                  <th class="text-center" scope="col">Hapus</th>
                </tr>
              </thead>
              <tbody>
                <tr
                  class="text-center"
                  v-for="(keranjang, index) in keranjangs"
                  :key="keranjang.id"
                >
                  <th class="text-center" style="vertical-align: middle">
                    {{ index + 1 }}
                  </th>
                  <td>
                    <img
                      :src="'../assets/images/' + keranjang.products.gambar"
                      class="img-fluid shadow"
                      style="width: 20vh"
                    />
                  </td>
                  <td class="text-center" style="vertical-align: middle">
                    {{ keranjang.products.nama }}
                  </td>
                  <td class="text-center" style="vertical-align: middle">
                    {{ keranjang.keterangan }}
                  </td>
                  <td class="text-center" style="vertical-align: middle">
                    {{ keranjang.jumlah_pemesanan }}
                  </td>
                  <td class="text-center" style="vertical-align: middle">
                    Rp. <strong> {{ keranjang.products.harga }} </strong>
                  </td>
                  <td class="text-center" style="vertical-align: middle">
                    Rp.
                    <strong
                      >{{
                        keranjang.products.harga * keranjang.jumlah_pemesanan
                      }}
                    </strong>
                  </td>
                  <td class="text-center" style="vertical-align: middle">
                    <b-icon-trash-fill
                      class="text-danger"
                      @click="hapusKeranjang(keranjang.id)"
                    ></b-icon-trash-fill>
                  </td>
                </tr>
                <tr>
                  <td style="border-bottom: none" colspan="6" align="right">
                    <strong>Total Harga : </strong>
                  </td>
                  <td style="border-bottom: none" align="center">
                    <strong>Rp. {{ totalHarga }}</strong>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>

      <!-- Check Out -->
      <div class="row justify-content-end">
        <div class="col-md-4">
          <form class="col" v-on:submit.prevent>
            <div class="form-group mt-3 mb-3">
              <label for="nama">Nama : </label>
              <input type="text" class="form-control" v-model="pesan.nama" />
            </div>
            <div class="form-group mt-3 mb-3">
              <label for="no_meja">Nomor Meja : </label>
              <input
                type="number"
                class="form-control"
                v-model="pesan.no_meja"
              />
            </div>
            <button
              type="submit"
              class="btn btn-success float-end"
              @click="checkout"
            >
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
  name: "KeranjangView",
  components: {
    Navbar,
  },
  data() {
    return {
      keranjangs: [],
      pesan: {},
    };
  },
  methods: {
    setKeranjangs(data) {
      this.keranjangs = data;
    },
    hapusKeranjang(id) {
      axios
        .delete("http://localhost:3000/keranjangs/" + id)
        .then(() => {
          this.$swal({
            title: "Berhasil Hapus Keranjang",
            icon: "error",
            timer: 3000,
            toast: true,
            position: "top-end",
            showConfirmButton: false,
            timerProgressBar: true,
          });
        })
        // Update data keranjangs // represh web
        .then(() => {
          axios
            .get("http://localhost:3000/keranjangs")
            .then((response) => this.setKeranjangs(response.data))
            .catch((error) => console.log(error));
        });
    },
    checkout() {
      if (this.pesan.nama && this.pesan.no_meja) {
        this.pesan.keranjangs = this.keranjangs;
        axios
          .post("http://localhost:3000/pesanans", this.pesan)
          .then(() => {
            // Hapus Semua Keranjang
            this.keranjangs.map(function (items) {
              return axios.delete(
                "http://localhost:3000/keranjangs/" + items.id
              );
            });

            this.$router.push({ path: "/pesanan-sukses" });
            this.$swal({
              title: "Sukses di Pesan",
              icon: "success",
              timer: 3000,
              toast: true,
              position: "top-end",
              showConfirmButton: false,
              timerProgressBar: true,
            });
          })
          .catch((error) => console.log(error));
      } else {
        this.$swal({
          title: "Nama dan No Meja Tolong di Isi",
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
      .get("http://localhost:3000/keranjangs")
      .then((response) => this.setKeranjangs(response.data))
      .catch((error) => console.log(error));
  },
  computed: {
    totalHarga() {
      return this.keranjangs.reduce(function (items, data) {
        return items + data.products.harga * data.jumlah_pemesanan;
      }, 0);
    },
  },
};
</script>

<style>
</style>