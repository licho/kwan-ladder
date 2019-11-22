<template>
  <div>
      <div v-for="(player, index) in players" :key="player.id" class="col-lg-4 mx-auto">
          <rung
            :id="player.id"
            :name="player.name"
            :avatarUrl="player.avatar_url"
            :position="player.position"
            :nextPlayer="players[index - 1]"
            :previousPlayer="players[index + 1]"
            @updated="getPlayers"/>
      </div>
  </div>
</template>

<script>
import Rung from './Rung.vue'

export default {
    name: 'ladder',
    components: {
        Rung
    },
    data () {
        return {
            players: []
        }
    },
    methods: {
        getPlayers() {
            fetch('http://localhost:3000/players?_sort=position')
            .then(response => {
                return response.json();
            })
            .then(players => {
                this.players = players;
            })
        }
    },
    created() {
        this.getPlayers();
    }
}
</script>

<style>

</style>