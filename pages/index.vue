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
      <div class="z-50 absolute top-0 right-0">
        <button type="button" class="bg-yellow-500 p-2 opacity-50 hover:opacity-100" @click="showPlayers = !showPlayers">
          <svg v-if="!showPlayers" xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
            <path stroke-linecap="round" stroke-linejoin="round" d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z" />
            <path stroke-linecap="round" stroke-linejoin="round" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
          </svg>
          <svg v-else xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
            <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
          </svg>
        </button>
      </div>
      <transition
        enter-active-class="transition ease-out duration-100"
        enter-from-class="transform opacity-0 scale-95"
        enter-to-class="transform opacity-100 scale-100"
        leave-active-class="transition ease-in duration-75"
        leave-from-class="transform opacity-100 scale-100"
        leave-to-class="transform opacity-0 scale-95"
      >
        <div v-if="showPlayers" class="fixed z-40 top-0 right-0 bottom-0 left-0 bg-black bg-opacity-90 text-white text-left p-4 overflow-y-auto overflow-x-hidden">
          <template v-if="teamOne.length">
            <div>
              <h6 class="font-bold text-lg">Tim 1</h6>
              <ul class="p-4 flex flex-col gap-2">
                <li v-for="(teamOnePlayer, teamOnePlayerIndex) in teamOne" :key="teamOnePlayer.id" class="flex items-center gap-4 justify-between" :class="{'pb-2 border-b border-white border-opacity-10': teamOnePlayerIndex === 4}">
                  <div class="flex items-center gap-4">
                    <img
                      class="w-10 h-10"
                      :src="`/images/player/${teamOnePlayer.id}.png`"
                      alt=""
                    />
                    {{teamOnePlayer.name}}
                  </div>
                  <div>
                    <button type="button" class="w-4 h-4 rounded-full" :class="[teamOnePlayer.active ? 'bg-green-500' : 'bg-red-500']" />
                  </div>
                </li>
              </ul>
            </div>
            <div>
              <h6 class="font-bold text-lg">Tim 2</h6>
              <ul class="p-4 flex flex-col gap-2">
                <li v-for="(teamTwoPlayer, teamTwoPlayerIndex) in teamTwo" :key="teamTwoPlayer.id"  class="flex items-center gap-4 justify-between" :class="{'pb-2 border-b border-white border-opacity-10': teamTwoPlayerIndex === 4}">
                  <div class="flex items-center gap-4">
                    <img
                      class="w-10 h-10"
                      :src="`/images/player/${teamTwoPlayer.id}.png`"
                      alt=""
                    />
                    {{teamTwoPlayer.name}}
                  </div>
                  <div>
                    <button type="button" class="w-4 h-4 rounded-full" :class="[teamTwoPlayer.active ? 'bg-green-500' : 'bg-red-500']" />
                  </div>
                </li>
              </ul>
            </div>
            <div v-if="teamThree.length">
              <h6 class="font-bold text-lg">Tim 3</h6>
              <ul class="p-4 flex flex-col gap-2">
                <li v-for="(teamThreePlayer, teamThreePlayerIndex) in teamThree" :key="teamThreePlayer.id"  class="flex items-center gap-4 justify-between" :class="{'pb-2 border-b border-white border-opacity-10': teamThreePlayerIndex === 4}">
                  <div class="flex items-center gap-4">
                    <img
                      class="w-10 h-10"
                      :src="`/images/player/${teamThreePlayer.id}.png`"
                      alt=""
                    />
                    {{teamThreePlayer.name}}
                  </div>
                  <div>
                    <button type="button" class="w-4 h-4 rounded-full" :class="[teamThreePlayer.active ? 'bg-green-500' : 'bg-red-500']" />
                  </div>
                </li>
              </ul>
            </div>
          </template>
          <button
            v-else
            type="button"
            class="inline-flex justify-center mt-10 py-2 px-4 w-full border border-transparent shadow-sm text-sm font-medium rounded-md text-white bg-blue-600 hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500"
            @click="onGenerateTeam()">Generiraj timove</button>
          <div style="margin-top: 20px">
            <h6 class="font-bold text-lg">Svi igrači</h6>
            <ul class="p-4 flex flex-col gap-2">
              <li v-for="player in players" :key="player.id" class="flex items-center gap-4 justify-between">
                <div class="flex items-center gap-4">
                  <img
                    class="w-10 h-10"
                    :src="`/images/player/${player.id}.png`"
                    alt=""
                  />
                  {{player.name}}
                </div>
                <div>
                  <button type="button" class="w-4 h-4 rounded-full" :class="[player.active ? 'bg-green-500' : 'bg-red-500']" @click="player.active = !player.active" />
                </div>
              </li>
            </ul>
          </div>
        </div>
      </transition>
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
    showPlayers: false,
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
  mounted() {
    // this.onGenerateTeam()
    if(localStorage.getItem('teamOne')) {
      this.teamOne = JSON.parse(localStorage.getItem('teamOne') as string)
    }
    if(localStorage.getItem('teamTwo')) {
      this.teamTwo = JSON.parse(localStorage.getItem('teamTwo') as string)
    }
    if(localStorage.getItem('teamThree')) {
      this.teamThree = JSON.parse(localStorage.getItem('teamThree') as string)
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
      localStorage.setItem('teamOne', JSON.stringify(this.teamOne))
      localStorage.setItem('teamTwo', JSON.stringify(this.teamTwo))
      localStorage.setItem('teamThree', JSON.stringify(this.teamThree))
    }
  }
})
</script>
