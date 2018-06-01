<template>
  <div>
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
                    ゲノグルスコア : <star-rating star-size="30" v-bind:increment="0.1" v-bind:rating=store.genome_point></star-rating>
                    平均点 : <star-rating star-size="30" active-color="#727272" v-bind:increment="0.1" v-bind:rating=store.ave_point></star-rating>
                  </div>
                </div>

                <!-- bottom -->
                <div class="content">
                  {{ store.pr }}
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="column">
          <div class="card">
            <div class="card-content">
              <p class="title is-4">同じ味覚の人から探す</p>
              <p class="subtitle is-6">味覚が合う人</p>
              <div class="content">
                ゲノムマップを利用して同じ味覚の人がオススメしているお店を表示します
                <br>
              </div>
              <a class="button is-warning">味覚が合う人</a>
            </div>
          </div>
          <div class="card">
            <div class="card-content">
              <p class="title is-4">同じ嗅覚の人から探す</p>
              <p class="subtitle is-6">嗅覚が合う人</p>
              <div class="content">
                ゲノムマップを利用して同じ嗅覚の人がオススメしているお店を表示します
                <br>
                <a class="button is-warning">嗅覚が合う人</a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
  import axios from 'axios'
  import StarRating from 'vue-star-rating'
  export default {
    components: {
      StarRating,
    },
    name: "card",
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

<style scoped>
  .search-bar {
    margin-top: 30px;
    margin-bottom: 30px;
  }
  #card {
    margin-bottom: 40px;
  }
</style>
