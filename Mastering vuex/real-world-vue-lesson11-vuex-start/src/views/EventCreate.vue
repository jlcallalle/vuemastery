<template>
  <div>
    <div class="box-state" style="display:none">
      <h1>Create Event - {{ $store.state.user.name }}</h1>
      <p>This event was created by {{ user.name }} with id: {{ user.id }}</p>
      <p><strong>Ejemplo Array Categorias</strong></p>
      <!-- <ul>
        <li v-for="cat in categories" :key="cat">{{ cat }}</li>
      </ul>
      <p>cantidad: {{ categories.length }}</p -->>
      <p>Getter: Hay {{ catLength }}</p>
      <p><strong>Ejemplo Array Todos</strong></p>
      <p>doneTodos {{ doneTodos }}</p>
      <p>doneTodactiveTodosCountos {{ activeTodosCount }}</p>
      <p><strong>Getters Dinámico</strong></p>
      <!-- <p>{{ getEvent(1) }} </p> -->
      <p>{{ getEventById(1) }}</p>
    </div>
    <br />
    <form @submit.prevent="createEvent">
      <label>Select a category</label>
      <select v-model="event.category">
        <option v-for="cat in categories" :key="cat">{{ cat }}</option>
      </select>

      <h3>Name & describe your event</h3>
      <div class="field">
        <label>Title</label>
        <input
          v-model="event.title"
          type="text"
          placeholder="Add an event title"
        />
      </div>

      <div class="field">
        <label>Description</label>
        <input
          v-model="event.description"
          type="text"
          placeholder="Add a description"
        />
      </div>

      <h3>Where is your event?</h3>
      <div class="field">
        <label>Location</label>
        <input
          v-model="event.location"
          type="text"
          placeholder="Add a location"
        />
      </div>

      <h3>When is your event?</h3>

      <div class="field">
        <label>Date</label>
        <datepicker v-model="event.date" placeholder="Select a date" />
      </div>

      <div class="field">
        <label>Select a time</label>
        <select v-model="event.time">
          <option v-for="time in times" :key="time">{{ time }}</option>
        </select>
      </div>

      <input type="submit" class="button -fill-gradient" value="Submit" />
    </form>
  </div>
</template>

<script>
import Datepicker from 'vuejs-datepicker'
import { mapState } from 'vuex'
import { mapGetters } from 'vuex'

export default {
  components: {
    Datepicker
  },
  data() {
    const times = []
    for (let i = 1; i <= 24; i++) {
      times.push(i + ':00')
    }
    return {
      times,
      categories: this.$store.state.categories,
      event: this.createFreshEventObject()
    }
  },
  methods: {
    createEvent() {
      this.$store
        .dispatch('createEvent', this.event)
        .then(() => {
          this.$router.push({
            name: 'event-show',
            params: { id: this.event.id }
          })
          this.event = this.createFreshEventObject()
        })
        .catch(() => {
          console.log('There was a problem creating your event')
        })
    },
    createFreshEventObject() {
      const user = this.$store.state.user
      const id = Math.floor(Math.random() * 10000000)

      return {
        id: id,
        user: user,
        category: '',
        organizer: user,
        title: '',
        description: '',
        location: '',
        date: '',
        time: '',
        attendees: []
      }
    }
  },
  computed: {
    ...mapGetters(['getEventById']),
    /* getEvent() {
      return this.$store.getters.getEventById
    }, */
    catLength() {
      //return this.$store.state.categories.length
      return this.$store.getters.catLength
    },
    doneTodos() {
      return this.$store.getters.doneTodos
    },
    activeTodosCount() {
      return this.$store.getters.activeTodosCount
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
.field {
  margin-bottom: 24px;
}
</style>
