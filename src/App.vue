<template>
  <div id="app">
    <my-title></my-title>
    <my-card></my-card>
    <my-footer></my-footer>
  </div>
</template>

<script>
  import MyTitle from './components/title.vue'
  import MyCard from './components/card.vue'
  import MyFooter from './components/footer.vue'

  export default {
    components: {
      MyTitle,
      MyCard,
      MyFooter,
    },
    name: 'app',
    data() {
      return {
      }
    },
    methods: {
    },
  }
</script>

<style>

</style>
