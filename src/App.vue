<template>
  <div id="app">

    <!-- title -->
    <section class="hero is-warning">
      <div class="hero-head">
        <div class="navbar">
          <div class="container">
            <div class="navbar-brand">
              <div class="navbar-item">
                <img src="./assets/logo1.png">
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


    <!-- search form -->
    <section class="search-bar">
      <div class="container">

        <div class="field has-addons">
          <div class="control">
            <input @keyup.enter="search" v-model="query" class="input" type="text" placeholder="食べたい料理">
          </div>
          <div class="control">
            <a @click="search" class="button is-warning">
              検索
            </a>
          </div>
        </div>
      </div>
    </section>


    <!-- card -->
    <div id="card" class="container">
      <div class="columns">
        <div class="column is-two-thirds">

          <div v-for="store in data">
            <div class="card">
              <div class="card-content">

                <!-- top -->
                <div class="columns">
                  <div class="column is-two-thirds">
                    <div class="media">
                      <div class="media-left">
                        <figure class="image is-128x128">
                          <img v-bind:src="store.image_url" alt="Placeholder image">
                        </figure>
                      </div>
                      <div class="media-content">
                        <p class="title is-4">{{ store.shop_name }}</p>
                        <p>平均金額 : ¥{{ store.cost }}</p>
                      </div>
                    </div>

                  </div>
                  <div class="column ">
                    平均点 : <star-rating star-size="30" v-bind:increment="0.1" v-bind:rating=store.ave_point></star-rating>
                    ゲノグルスコア : <star-rating star-size="30" v-bind:increment="0.1" v-bind:rating=store.genome_point></star-rating>
                  </div>
                </div>

                <!-- bottom -->
                <div class="content">
                  {{ store.pr }}
                  <a href="#">#css</a> <a href="#">#responsive</a>
                  <br>
                  <time datetime="2016-1-1">11:09 PM - 1 Jan 2016</time>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="column">
          <div class="card">
            <div class="card-content">
              <p class="title is-4">エリアから探す</p>
              <p class="subtitle is-6">地図を検索</p>
              <div class="content">
                Lorem ipsum dolor sit amet, consectetur adipiscing elit.
                Phasellus nec iaculis mauris. <a>@bulmaio</a>.
                <a href="#">#css</a> <a href="#">#responsive</a>
                <br>
                <time datetime="2016-1-1">11:09 PM - 1 Jan 2016</time>
              </div>
            </div>
          </div>
          <div class="card">
            <div class="card-content">
              <p class="title is-4">ジャンルから探す</p>
              <p class="subtitle is-6">ジャンルを指定</p>
              <div class="content">
                Lorem ipsum dolor sit amet, consectetur adipiscing elit.
                Phasellus nec iaculis mauris. <a>@bulmaio</a>.
                <a href="#">#css</a> <a href="#">#responsive</a>
                <br>
                <time datetime="2016-1-1">11:09 PM - 1 Jan 2016</time>
              </div>
            </div>
          </div>
        </div>
      </div>

    </div>


    <!-- footer -->
    <footer class="footer">
      <div class="container">
        <div class="content has-text-centered">
          <p>
            <strong>Genoguru</strong> by <a href="https://jgthms.com">Team X</a>. The source code is licensed
            <a href="http://opensource.org/licenses/mit-license.php">MIT</a>. The website content
            is licensed <a href="http://creativecommons.org/licenses/by-nc-sa/4.0/">CC BY NC SA 4.0</a>.
          </p>
        </div>
      </div>
    </footer>

  </div>
</template>

<script>
  import axios from 'axios'
  import StarRating from 'vue-star-rating'

  export default {
    components: {
      StarRating
    },
    name: 'app',
    data() {
      return {
        query: '',
        data: [
        ],
      }
    },
    methods: {
      search: function () {
        axios.get(`https://genoguru2018.herokuapp.com/api/search?freeword=${this.query}`)
          .then(response => {
            this.data = response.data.items;
            console.log(response)

          })
          .catch(e => {
            console.log(e);
          })

      },
    },
  }
</script>

<style>
  .navbar-item img {
    max-height: 7em;
  }
  .bigNum {
    font-size: 1em;
  }

  .bigStr {
    font-size: 1em;
  }

  .search-bar {
    margin-top: 30px;
    margin-bottom: 30px;
  }

  #card {
    margin-bottom: 40px;
  }

  #table {
    margin-bottom: 100px;
  }
</style>
