<template>
  <div>
    <h1>Events</h1>
    <EventCard
      v-for="(event, index) in events"
      :key="index"
      :event="event"
      :data-index="index"
    />
  </div>
</template>

<script>
import EventCard from "../components/EventCard.vue";
// import EventService from "../services/EventService.js";
import { mapState } from "vuex";

export default {
  head() {
    return {
      title: "Event Listing"
    };
  },
  components: {
    EventCard
  },
  // asyncData({ $axios, error }) {
  //   return $axios
  //     .get("http://localhost:3001/events")
  //     .then(response => {
  //       return {
  //         events: response.data
  //       };
  //     })
  //     .catch(e => {
  //       error({
  //         statusCode: 503,
  //         message: "Unable to fetch events at this time. Please try again."
  //       });
  //     });
  // },

  // async asyncData({ $axios, error }) {
  //   try {
  //     const { data } = await $axios.get("http://localhost:3001/events");

  //     return {
  //       events: data
  //     };
  //   } catch (err) {
  //     error({
  //       statusCode: 503,
  //       message: "Unable to fetch events at this time. Please try again."
  //     });
  //   }
  // }

  // async asyncData({ error }) {
  //   try {
  //     const { data } = await EventService.getEvents();

  //     return {
  //       events: data
  //     };
  //   } catch (err) {
  //     error({
  //       statusCode: 503,
  //       message: "Unable to fetch events at this time. Please try again."
  //     });
  //   }
  // }

  // using Vuex
  async fetch({ store, error }) {
    try {
      await store.dispatch("events/fetchEvents");
    } catch (err) {
      error({
        statusCode: 503,
        message: "Unable to fetch events at this time. Please try again."
      });
    }
  },

  computed: mapState({
    events: state => state.events.events
  })
};
</script>
