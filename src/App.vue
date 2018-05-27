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


    <!-- table -->
    <section id="table">
      <div class="container">
        <b-table :data="data" :columns="columns">

          <template slot-scope="props">

            <b-table-column width="40">
              <img v-bind:src="props.row.image" alt="">
            </b-table-column>
            <b-table-column width="40">
              <span class="bigStr">{{ props.row.storeName }}</span>
            </b-table-column>
            <b-table-column width="40">
              <span class="bigNum">{{ props.row.avg }}</span>
            </b-table-column>
            <b-table-column width="40">
              <span class="bigNum">{{ props.row.genomeAvg }}</span>
            </b-table-column>

          </template>

        </b-table>
      </div>
    </section>


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

  export default {
    name: 'app',
    data() {
      return {
        query: '',
        data: [
          {
            'storeName': '泰明軒',
            'avg': 3,
            'genomeAvg': 4,
            'image': 'https://tblg.k-img.com/restaurant/images/Rvw/82109/150x150_square_82109277.jpg'
          },
        ],
        columns: [
          {
            field: 'image',
            label: '写真'
          },
          {
            field: 'storeName',
            label: '店名',
          },
          {
            field: 'avg',
            label: '平均',
          },
          {
            field: 'genomeAvg',
            label: 'ゲノム平均',
          },
          {
            field: 'address',
            label: '住所'
          },
          {
            field: 'tel',
            label: '電話'
          },
          {
            field: 'catchCopy',
            label: 'キャッチコピー'
          },
          {
            field: 'price',
            label: '料金'
          },
        ],
        zipcode: '248-0011',
      }
    },
    methods: {
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
    margin-top: 60px;
    margin-bottom: 30px;
  }

  #table {
    margin-bottom: 100px;
  }
</style>
