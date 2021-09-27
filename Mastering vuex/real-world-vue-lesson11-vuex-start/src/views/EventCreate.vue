<template>
  <div>
    <h1>Create Event - {{ $store.state.user.name }}</h1>
    <p>This event was created by  {{ user.name }} with id: {{ user.id }}</p>
    <ul>
      <li v-for="cat in categories" :key="cat"> {{ cat }}</li>
    </ul>
  </div>
</template>

<script>
import { mapState } from 'vuex'

export default {
  computed: {
    localComputed() {
      return something
    },
    ...mapState(['categories', 'user'])
  }
 /*  computed: mapState(['categories', 'user']) */
 
/*   computed: mapState ({
    user: 'user',
    categories: 'categories'
  }) */
/*   computed: mapState ({
    userName: state => state.user.name,
    userId: state => state.user.id,
    categories: state => state.categories
  }) */
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
