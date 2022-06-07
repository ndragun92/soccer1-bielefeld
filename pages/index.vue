<template>
  <div class="bg-[#00a000] min-h-screen">
    <el-field :team-one="teamOne" :team-two="teamTwo" :team-three="teamThree" />
    <div class="text-center">
      <button
              type="button"
              class="inline-flex justify-center py-2 px-4 border border-transparent shadow-sm text-sm font-medium rounded-md text-white bg-blue-600 hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500"
              @click="onGenerateTeam()">Generiraj timove</button>
    </div>
    <div class="mt-4 text-center my-2 bg-black pt-6">
      <img class="w-20 m-auto" src="/images/soccer1-logo.png" alt="">
      <p class="mt-4 text-sm text-white">
        Schelpmilser Weg 11, 33609 Bielefeld
      </p>
      <div class="mt-6">
        <iframe src="https://www.google.com/maps/embed?pb=!1m14!1m8!1m3!1d9816.753055597379!2d8.6039907!3d52.039884!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x0%3A0xacfbe39223df076a!2sSoccer%201!5e0!3m2!1sen!2sde!4v1654606055530!5m2!1sen!2sde" width="100%" height="450" style="border:0;" allowfullscreen="" loading="lazy" referrerpolicy="no-referrer-when-downgrade"></iframe>
      </div>
<!--      <hr>-->
<!--      <pre>{{teamOne.length}}</pre>-->
<!--      <hr>-->
<!--      <pre>{{teamTwo.length}}</pre>-->
<!--      <hr>-->
<!--      <pre>{{teamThree.length}}</pre>-->
<!--      <hr>-->
<!--      <pre>{{teamOne}}</pre>-->
<!--      <hr>-->
<!--      <pre>{{teamTwo}}</pre>-->
<!--      <hr>-->
<!--      <pre>{{teamThree}}</pre>-->
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
      {id: 1, name: 'Mario', active: true, won: 0, lost: 0},
      {id: 2, name: 'Misko', active: true, won: 0, lost: 0},
      {id: 3, name: 'Dusko', active: true, won: 0, lost: 0},
      {id: 4, name: 'Nemanja', active: true, won: 0, lost: 0},
      {id: 5, name: 'Andrej', active: true, won: 0, lost: 0},
      {id: 6, name: 'Beco', active: true, won: 0, lost: 0},
      {id: 7, name: 'Niđo', active: true, won: 0, lost: 0},
      {id: 8, name: 'Kico', active: true, won: 0, lost: 0},
      {id: 9, name: 'Martin', active: true, won: 0, lost: 0},
      {id: 10, name: 'Teo', active: true, won: 0, lost: 0},
      {id: 11, name: 'Nikola R.', active: true, won: 0, lost: 0},
      {id: 12, name: 'Nikola V.', active: true, won: 0, lost: 0},
      {id: 13, name: 'Jozo', active: true, won: 0, lost: 0},
      {id: 14, name: 'Davor', active: true, won: 0, lost: 0},
      {id: 15, name: 'Danco', active: false, won: 0, lost: 0},
    ],
    teamOne: [] as {id: number, name: string, active: boolean, won: number, lost: number}[],
    teamTwo: [] as {id: number, name: string, active: boolean, won: number, lost: number}[],
    teamThree: [] as {id: number, name: string, active: boolean, won: number, lost: number}[],
    addedToTeam: 0
  }),
  computed: {
    returnFilteredPlayers() {
      return this.players.filter(player => player.active)
    }
  },
  methods: {
    randomIntFromInterval(min: number, max: number) { // min and max included
      return Math.floor(Math.random() * (max - min + 1) + min)
    },
    onGenerateTeam() {
      this.teamOne = []
      this.teamTwo = []
      this.teamThree = []
      shuffle(this.returnFilteredPlayers).forEach(player => {
        const minTeams = 1
        let maxTeams = 2
        if(this.returnFilteredPlayers.length >= 15) {
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
