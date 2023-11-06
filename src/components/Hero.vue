<template>
  <div class="hero">
    <!-- Dekstop -->
    <div class="d-none d-md-block">
      <div class="row mt-5">
        <div class="col-md-6">
          <div class="d-flex h-100">
            <div class="justify-content-center align-self-center">
              <h2>
                <strong>Delicious Foods Menu,</strong> <br />
                in Your Gadget
              </h2>
              <p>Ayo Segera pilih makanan favorit Anda</p>
              <button class="btn btn-lg btn-success">
                <b-icon-arrow-right></b-icon-arrow-right>
                <router-link
                  to="/foods"
                  style="color: white; text-decoration: none"
                  >Pesan</router-link
                >
              </button>
            </div>
          </div>
        </div>
        <div class="col-md-6">
          <img src="../assets/UnDraw-Eating.png" alt="" width="75%" />
        </div>
      </div>
    </div>

    <!-- Mobile -->
    <div class="d-sm-block d-md-none">
      <div class="col-md-6">
        <img src="../assets/UnDraw-Eating.png" alt="" width="100%" />
      </div>
      <div class="row mt-5 d-sm-block d-md-none">
        <div class="col-md-6">
          <div class="d-flex h-100">
            <div class="justify-content-center align-self-center">
              <h2>
                <strong>Delicious Foods Menu,</strong> <br />
                in Your Gadget
              </h2>
              <p>Ayo Segera pilih makanan favorit Anda</p>
              <button class="btn btn-lg btn-success">
                <b-icon-arrow-right></b-icon-arrow-right>
                Pesan
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "appHero",
};
</script>

<style>
</style>