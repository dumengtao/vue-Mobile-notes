<template>
  <div id="app">
    <v-select></v-select>
    <v-list></v-list>
    <v-content></v-content>
  </div>
</template>

<script type="ecmascript-6">
  import select from './components/select.vue'
  import list from './components/list.vue'
  import content from './components/content.vue'

  export default {
    name: 'app',
    components: {
      'v-select': select,
      'v-list': list,
      'v-content': content
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  #app
    font-family 'Helvetica Neue',Helvetica,Arial,sans-serif
    -webkit-font-smoothing antialiased
    -moz-osx-font-smoothing grayscale
    text-align center
</style>
