<template lang="pug">
  thead
    tr
      th(
        v-for="title in titles"
        @click="$emit('sort', $event)"
      ) {{title.toUpperCase()}} &#8593;
        sup A
</template>
<script>
export default {
  name: 'v-thead',
  props: {
    titles: {
      type: Array
    }
  }
}
</script>
