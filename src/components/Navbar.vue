<template>
  <div class="container">
    <b-navbar toggleable="lg" type="light" variant="faded">
      <b-navbar-brand>KuliNear</b-navbar-brand>
      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
      <b-collapse id="nav-collapse" is-nav>
        <!-- nav left -->
        <b-navbar-nav>
          <b-nav-item
            ><router-link class="nav-link" to="/">Home</router-link></b-nav-item
          >
          <b-nav-item
            ><router-link class="nav-link" to="/foods"
              >Foods</router-link
            ></b-nav-item
          >
        </b-navbar-nav>
        <!-- nav right -->
        <b-navbar-nav style="margin-left: auto">
          <b-nav-item
            ><router-link class="nav-link" to="/keranjang"
              ><strong
                >Keranjang<b-icon-cart></b-icon-cart>
                <span style="margin-left: 2px">{{
                  updateKeranjangs
                    ? updateKeranjangs.length
                    : jumlah_pesanans.length
                }}</span></strong
              ></router-link
            ></b-nav-item
          >
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>


<script>
import axios from "axios";
export default {
  name: "appNavbar",
  data() {
    return {
      jumlah_pesanans: [],
    };
  },
  props: ["updateKeranjangs"],
  methods: {
    setJumlah(data) {
      this.jumlah_pesanans = data;
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/keranjangs")
      .then((response) => this.setJumlah(response.data))
      .catch((error) => console.log(error));
  },
};
</script>

<style>
</style>