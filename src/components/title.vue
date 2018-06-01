<template>
  <div>
    <section class="hero is-warning">
      <div class="hero-head">
        <div class="navbar">
          <div class="container">
            <div class="navbar-brand">
              <div class="navbar-item">
                <img src="../assets/logo3.png">
              </div>
            </div>
            <div id="title" class="hero-body">
              <div class="container">
                <h1 class="title">
                  Genoguru
                </h1>
                <h2 class="subtitle">
                  好みが合う人がオススメする美味しいお店
                </h2>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
  export default {
    name: "title"
  }
</script>

<style scoped>
  .hero.is-warning .title {
    color: #727272
  }
  .hero.is-warning .subtitle {
    color: #727272
  }
  .navbar-item img {
    max-height: 7em;
  }

</style>
