<template lang="pug">
  tbody
    tr(
      v-for="item in endData"
      @dblclick.capture="$emit('edit', $event)"
      @keyup.enter="$emit('update', $event)"
      :id="item.id"
    )
      td
        input(
          readonly="readonly"
          :value="item.name"
          data-key="name"
        )
      td
        input(
          readonly="readonly"
          :value="item.location"
          data-key="location"
        )
      td
        input(
          readonly="readonly"
          :value="item.currency"
          data-key="currency"
          @input="isNum"
        )
</template>
<script>
export default {
  name: 'v-tbody',
  props: {
    endData: {
      type: Array
    }
  },
  methods: {
    isNum (e) {
      const val = e.target.value
      if (val.trim() === '') return
      if (!Number.isInteger(parseInt(val))) e.target.value = ''
    }
  }
}
</script>
