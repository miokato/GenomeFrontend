<template>
  <div id="app">

    <!-- title -->
    <section class="hero is-warning">
      <div id="title" class="hero-body">
        <div class="container">
          <h1 class="title">
            GenoGuru
          </h1>
          <h2 class="subtitle">
            Food recommendation system by Genome map
          </h2>
        </div>
      </div>
    </section>


    <!-- search bar -->
    <section class="search-bar">
      <div class="container">
        <div class="field has-addons">
          <div class="control">
            <input @keyup.enter="search" v-model="query"
                   class="input" type="text" placeholder="Search">
          </div>
          <div class="control">
            <a @click="search" class="button is-warning">
              Search
            </a>
          </div>
        </div>
      </div>
    </section>


    <!-- table -->
    <section>
      <b-table :data="data" :columns="columns"></b-table>
    </section>

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
        axios.get(`http://api.zipaddress.net/?zipcode=${this.query}`)
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
</style>
