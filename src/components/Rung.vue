<template>
  <b-card :img-src="avatarUrl" img-alt="Card image" img-left class="mt-3">
      <b-card-text>
        {{name}}
      </b-card-text>
      <div class="position">
          {{position}}
      </div>
      <div class="controls invisible">
        <b-button v-if="position < 24" variant="danger" class="mr-3" @click="stepDown">Bajar</b-button>
        <b-button v-if="position > 1" variant="success" @click="stepUp">Subir</b-button>
      </div>
    </b-card>
</template>

<script>
export default {
    name: 'rung',
    props: ['id', 'name', 'avatarUrl', 'position', 'nextPlayer', 'previousPlayer'],
    methods: {
        stepUp () {
            const newPosition = this.position - 1;
            const opponentNewPosition = this.nextPlayer.position + 1;
            this.updatePlayers(newPosition, this.nextPlayer, opponentNewPosition)
        },

        stepDown () {
            const newPosition = this.position + 1;
            const opponentNewPosition = this.previousPlayer.position - 1;
            this.updatePlayers(newPosition, this.previousPlayer, opponentNewPosition)
        },

        updatePlayers (userNewPosition, opponentToUpdate, opponentNewPosition) {
            this.putPlayer({
                id: this.id,
                name: this.name,
                avatar_url: this.avatarUrl,
                position: userNewPosition
            }).then(() => {
                return this.putPlayer({
                    id: opponentToUpdate.id,
                    name: opponentToUpdate.name,
                    avatar_url: opponentToUpdate.avatar_url,
                    position: opponentNewPosition
                })
            }).then(() => {
                this.$emit('updated')
            })
        },

        putPlayer (player) {
            return fetch('http://localhost:3000/players/' + player.id, {
                method: 'PUT',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(player)
            })
        }
    }
}
</script>

<style lang="less">
    .card {
        &:hover {
            .controls {
                visibility: visible !important;
            }
        }
    }

    .card-img-left {
        height: 150px;
        width: 150px;
    }

    .card-text {
        font-size: 20px;
        margin-top: 40px;
        text-align: left;
    }

    .position {
        position: absolute;
        right: 40px;
        color: #FC671B;
        font-size: 40px;
        top: 50px;
    }
</style>