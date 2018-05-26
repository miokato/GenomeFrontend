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
        <b-table :data="data" :columns="columns"></b-table>
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
        data: [],
        columns: [
          {
            field: 'pref',
            label: '店名',
          },
          {
            field: 'address',
            label: '食品名',
          },
          {
            field: 'city',
            label: '市',
          },
          {
            field: 'town',
            label: '町名'
          },
          {
            field: 'fullAddress',
            label: '住所'
          }
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
  .search-bar {
    margin-top: 60px;
    margin-bottom: 30px;
  }

  #table {
    margin-bottom: 300px;
  }
</style>
