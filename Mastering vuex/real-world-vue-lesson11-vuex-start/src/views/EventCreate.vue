<template>
  <div>
    <h1>Create Event - {{ $store.state.user.name }}</h1>
    <p>This event was created by  {{ userName }} with id: {{ userId }}</p>
  </div>
</template>

<script>
import { mapState } from 'vuex'

export default {
  computed: mapState ({
    userName: state => state.user.name,
    userId: state => state.user.id,
    categories: state => state.categories
  })
/*   computed: {
    userName() {
      return this.$store.state.user.name
    },
    userId() {
      return this.$store.state.user.id
    }
  } */
}
</script>

<style scoped>
</style>
