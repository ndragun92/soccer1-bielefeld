<template>
  <div class="bg-[#00a000] min-h-screen">
    <el-field />
    <div>
      <button type="button" @click="onGenerateTeam()">Generate team</button>
    </div>
    <div class="text-center my-2">
      <img class="w-20 m-auto" src="/images/soccer1-logo.png" alt="">
      <p class="mt-2 text-sm text-white">
        Schelpmilser Weg 11, 33609 Bielefeld
      </p>
      <hr>
      <pre>{{teamOne.length}}</pre>
      <hr>
      <pre>{{teamTwo.length}}</pre>
      <hr>
      <pre>{{teamThree.length}}</pre>
      <hr>
      <pre>{{teamOne}}</pre>
      <hr>
      <pre>{{teamTwo}}</pre>
      <hr>
      <pre>{{teamThree}}</pre>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import shuffle from 'lodash/shuffle'

export default Vue.extend({
  name: 'IndexPage',
  data: () => ({
    players: [
      {id: 1, name: 'Player 1', active: true, won: 0, lost: 0},
      {id: 2, name: 'Player 2', active: true, won: 0, lost: 0},
      {id: 3, name: 'Player 3', active: true, won: 0, lost: 0},
      {id: 4, name: 'Player 4', active: true, won: 0, lost: 0},
      {id: 5, name: 'Player 5', active: true, won: 0, lost: 0},
      {id: 6, name: 'Player 6', active: true, won: 0, lost: 0},
      {id: 7, name: 'Player 7', active: true, won: 0, lost: 0},
      {id: 8, name: 'Player 8', active: true, won: 0, lost: 0},
      {id: 9, name: 'Player 9', active: true, won: 0, lost: 0},
      {id: 10, name: 'Player 10', active: true, won: 0, lost: 0},
      {id: 11, name: 'Player 11', active: true, won: 0, lost: 0},
      {id: 12, name: 'Player 12', active: true, won: 0, lost: 0},
      {id: 13, name: 'Player 13', active: true, won: 0, lost: 0},
      // {id: 14, name: 'Player 14', active: true, won: 0, lost: 0},
      // {id: 15, name: 'Player 15', active: true, won: 0, lost: 0},
      // {id: 16, name: 'Player 16', active: true, won: 0, lost: 0},
    ],
    teamOne: [] as {id: number, name: string, active: boolean, won: number, lost: number}[],
    teamTwo: [] as {id: number, name: string, active: boolean, won: number, lost: number}[],
    teamThree: [] as {id: number, name: string, active: boolean, won: number, lost: number}[],
    addedToTeam: 0
  }),
  methods: {
    randomIntFromInterval(min: number, max: number) { // min and max included
      return Math.floor(Math.random() * (max - min + 1) + min)
    },
    onGenerateTeam() {
      this.teamOne = []
      this.teamTwo = []
      this.teamThree = []
      shuffle(this.players).forEach(player => {
        const minTeams = 1
        let maxTeams = 2
        if(this.players.length >= 15) {
          maxTeams = 3
        }
        if(!this.addedToTeam) {
          const team = this.randomIntFromInterval(minTeams, maxTeams)
          switch (team) {
            case 1:
              this.teamOne.push(player)
              break
            case 2:
              this.teamTwo.push(player)
              break
            case 3:
              this.teamThree.push(player)
              break
          }
          this.addedToTeam = team
        } else if(maxTeams === 3) {
            switch (this.addedToTeam) {
              case 1:
                this.teamTwo.push(player)
                this.addedToTeam = 2
                break
              case 2:
                this.teamThree.push(player)
                this.addedToTeam = 3
                break
              case 3:
                this.teamOne.push(player)
                this.addedToTeam = 1
                break
            }
          } else {
            switch (this.addedToTeam) {
              case 1:
                this.teamTwo.push(player)
                this.addedToTeam = 2
                break
              case 2:
                this.teamOne.push(player)
                this.addedToTeam = 1
                break
            }
          }
      })
    }
  }
})
</script>
