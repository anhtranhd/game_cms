<template>
  <section class="section">
    <div class="container">
      <div class="columns">
        <div class="column is-4 is-offset-4">
          <h2 class="title has-text-centered">List Game</h2>

          <Notification :message="error" v-if="error"/>

          <div v-for="game in games" :key="game.id">
            <div>{{ game.id }}</div>

<!--            <v-data-table-->
<!--              :headers="headers"-->
<!--              :items="games"-->
<!--              item-key="name"-->
<!--              class="elevation-1"-->
<!--            >-->
<!--            </v-data-table>-->
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import Notification from '~/components/Notification'
import axios from 'axios'

export default {
  components: {
    Notification,
  },

  // async asyncData() {
  //   const { data } = await axios.get('https://api.8668live.com/api/v1.0/rooms/list_game')
  //   return {
  //     games : data
  //   }
  // },


  async asyncData({ $axios }) {

    try {
      const datas = await $axios.$get('https://api.8668live.com/api/v1.0/rooms/list_game')
      const games = datas.data
      return { games }
    } catch (e) {
      this.error = e.response.data.message
    }
  },

  data() {
    return {
      games: null,
      headers: [
        {
          text: 'AAA',
          value: 'turn',
        },
        {
          text: 'BBB',
          value: 'players',
        }
      ]
    }
  },

  methods: {
    // async asyncData() {
    //   const games  = await this.axios.$get('https://api.8668live.com/api/v1.0/rooms/list_game')
    //   this.games = games;
    // },
  },
  middleware: 'auth',
}
</script>
