<template>
  <div class="container">
    <Navbar />
    <!-- Dekstop -->
    <div class="d-none d-md-block">
      <div class="row mt-2">
        <div class="col-md-6">
          <div class="d-flex h-100">
            <div class="justify-content-center align-self-center">
              <h2>
                <strong>Pesanan Sukses di Buat,</strong> <br />
                Pesanan Anda Segera di Proses
              </h2>
            </div>
          </div>
        </div>
        <div class="col-md-6">
          <img src="../assets/menunggu.png" alt="" width="100%" />
        </div>
      </div>
    </div>

    <!-- Mobile -->
    <div class="d-sm-block d-md-none">
      <div class="col-md-6">
        <img src="../assets/menunggu.png" alt="" width="100%" />
      </div>
      <div class="row mt-5 d-sm-block d-md-none">
        <div class="col-md-6">
          <div class="d-flex h-100">
            <div class="justify-content-center align-self-center">
              <h2>
                <strong>Pesanan Sukses di Buat,</strong> <br />
                Pesanan Anda Segera di Proses
              </h2>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
export default {
  name: "PesananSuksesView",
  components: {
    Navbar,
  },
};
</script>

<style>
</style>