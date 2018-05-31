<template lang="pug">
  input(
    :placeholder="placeholder"
    @input="$emit('search', $event)"
    :class="compClass"
  )
</template>

<script>
export default {
  name: 'v-search',
  props: {
    placeholder: {
      type: String,
      default: 'Search'
    },
    compClass: {
      type: String,
      default: 'search'
    }
  }
}
</script>

<style lang="sass"></style>
