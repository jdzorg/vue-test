<template lang="pug">
  #app
    v-data-table(
      :items="mockData"
      class="elevation-1"
    )
      template(
        slot="items"
        slot-scope="props"
        data-id="props.item.id"
      )
        td {{props.item.name}}
        td(class="text-xs-right") {{props.item.location}}
        td(class="text-xs-right") {{props.item.currency}}
</template>

<script>
import mockData from './assets/test.json'

export default {
  name: 'App',
  components: {
  },
  data () {
    return {
      mockData: mockData
    }
  }
}
</script>

<style lang="sass">
#app
  font-family: 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
  text-align: center
  color: #2c3e50
  margin-top: 60px

</style>
