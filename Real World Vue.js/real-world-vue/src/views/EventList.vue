<template>
  <div>
    <h1>Events Listing</h1>
    <EventCard v-for="event in events" :key="event.id" :event="event"/>
    <BaseIcon />
  </div>
</template>

<script>
import EventCard from '@/components/EventCard.vue'
// import axios from 'axios'
import EventService from '@/services/EventService.js'

export default {
  components: {
    EventCard
  },
  data() {
    return {
      events: []
    }
  },
   created() {
      // axios
      //   .get('http://localhost:3000/events') 
      EventService.getEvents()
        .then(response => {
          console.log(response.data,'load data')
          this.events = response.data // <--- set the events data
        })
        .catch(error => {
          console.log('There was an error:', error.response)
        })
    }
}
</script>

<style lang="scss" scoped></style>
