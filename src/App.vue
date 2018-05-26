<template>
  <div id="app">
    <div class="container">
      <!-- search bar -->
      <div class="field has-addons is-clearfix">
        <div class="control">
          <input @keyup.enter="search" v-model="query"
                 class="input" type="text" placeholder="Search">
        </div>
        <div class="control">
          <a @click="search" class="button is-info">
            Search
          </a>
        </div>
      </div>

      <!-- table -->
      <b-table :data="data" :columns="columns"></b-table>
    </div>
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
  #app {
    margin-top: 60px;
  }
</style>
