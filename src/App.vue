<template>
  <div id="app">

    <!-- title -->
    <section class="hero is-warning">
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
                  <div class="column is-two-fifths">
                    <div class="media">
                      <div class="media-left">
                        <figure class="image is-128x128">
                          <img v-bind:src="store.image" alt="Placeholder image">
                        </figure>
                      </div>
                      <div class="media-content">
                        <p class="title is-4">{{ store.storeName }}</p>
                        <p class="is-6">点数 : {{ store.avg }}</p>
                        <p class="is-6">ゲノム点数 : {{ store.genomeAvg }}</p>
                        <p>金額 : {{ store.price }}</p>
                      </div>
                    </div>

                  </div>
                  <div class="column ">
                    点数 : <star-rating star-size="30" rating="3"></star-rating>
                    ゲノム点数 : <star-rating star-size="30" rating="2"></star-rating>
                  </div>
                </div>

                <!-- bottom -->
                <div class="content">
                  {{ store.message }}
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
          {
            'storeName': 'ウイウイ',
            'message': '地下の完全プライベート空間でパーティー可能★8名様から貸切OK！女子会・歓送迎会に…♪',
            'address': '[東京] 新富町駅 281m / ダイニングバー、居酒屋、ワインバー',
            'price': '¥4000 ~ ¥8000',
            'rating': 3,
            'genomeAvg': 4,
            'image': 'https://tblg.k-img.com/restaurant/images/Rvw/82109/150x150_square_82109277.jpg'
          },
          {
            'storeName': 'まるごと北海道 浅草店',
            'message': 'チャーハンが最高',
            'address': '[東京] 浅草（つくばＥＸＰ）駅 18m / かに、郷土料理（その他',
            'price': '¥3000 ~ ¥9000',
            'avg': 3,
            'genomeAvg': 4,
            'image': 'https://tblg.k-img.com/restaurant/images/Rvw/78630/150x150_square_78630548.jpg',
          },
        ],
      }
    },
    methods: {
      setRating: function(rating) {
        this.rating = rating;
      },
      search: function () {
        axios.get(`https://api.zipaddress.net/?zipcode=${this.query}`)
          .then(response => {
            this.data = [response.data.data];

          })
          .catch(e => {
            this.errors.push(e)
          })

      },
    },
  }
</script>

<style>
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
