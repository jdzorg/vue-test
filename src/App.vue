<template lang="pug">
  #app
    v-search(
      @search="search"
    )
    .currency-sum Currency sum
      b {{ currencySum }}
    .table-wrapper
      .hint double click to edit.
        br
        | To update press Enter
      table
        v-thead(
          :titles="titles"
          @sort="sort"
        )
        v-tbody(
          :end-data="endData"
          @edit="edit"
          @update="update"
        )
</template>

<script>
import mockData from './assets/test.json'
import helpers from './assets/js/utils'

import VSearch from './components/VSearch'
import VThead from './components/VThead'
import VTbody from './components/VTbody'

export default {
  name: 'App',
  components: {
    VTbody,
    VThead,
    VSearch
  },
  data () {
    return {
      searched: '',
      endData: [],
      mockData: mockData,
      titles: ['name', 'location', 'currency'],
      curEditID: null
    }
  },
  computed: {
    currencySum () {
      return this.endData
        .map(item => item.currency)
        .reduce((prev, cur) => parseInt(prev) + parseInt(cur))
    }
  },
  methods: {
    search (e) {
      const searchFor = e.target.value.toString().toLowerCase()
      if (searchFor.trim() === '') this.endData = this.mockData

      const _includes = helpers._includes
      this.endData = this.mockData.filter(item => {
        if (_includes(item.name, searchFor) || _includes(item.location, searchFor) || _includes(item.currency, searchFor)) return item
      })
    },
    sort (e) {
      const colName = e.target.innerText.split(' ')[0].toLowerCase()
      this.endData.sort((a, b) => (a[colName] > b[colName]) ? 1 : ((b[colName] > a[colName]) ? -1 : 0))
    },
    edit (e) {
      this.curEditID = e.currentTarget.id
      const curInput = e.target
      curInput.readOnly = false
    },
    update (e) {
      const curInput = e.target
      curInput.readOnly = true
      const curID = this.curEditID
      this.endData
        .forEach(item => {
          if (item.id.toString().includes(curID)) {
            item[curInput.dataset.key] = curInput.value
          }
        })
    }
  },
  beforeMount () {
    this.endData = this.mockData
  }
}
</script>

<style lang="sass">
#app
  font-family: 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
  color: #2c3e50
  margin-top: 60px

  input
    padding: .3rem
    border:
      top: none
      left: none
      right: none

  .search
    font-size: 1.2rem
    margin-bottom: 1rem

  .currency-sum b
    color: red
    padding-left: .5rem

  .table-wrapper
    margin-top: 1.1rem
    position: relative
    z-index: 1
    &:hover .hint
      opacity: 1
    .hint
      display: block
      opacity: 0
      position: absolute
      z-index: 2
      top: 3%
      right: 40%
      transition: .2s ease

    thead th
      cursor: pointer
      sup
        font-size: .5rem
    /*tbody*/
      /*td */
</style>
