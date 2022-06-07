<template>
  <div class="w-full h-full">
    <img
      class="w-96 m-auto"
      src="~static/images/football_field.svg"
      alt="Soccer field"
    />
    <div class="absolute top-[1.1rem] w-full">
      <div
        class="bg-black bg-opacity-25 text-white w-[21.7rem] h-[16.95rem] m-auto"
      >
        <div
          v-if="topTeamSelected"
          class="h-6 px-4 font-bold text-center flex items-center justify-center gap-2"
        >
          <h6 class="mt-0.5">Tim</h6>
          <div
            class="mt-0.5 relative inline-block text-left"
            :class="{ 'pointer-events-none': !teamThree.length }"
          >
            <div>
              <button
                id="menu-button"
                type="button"
                class="inline-flex justify-center w-full rounded-md border-none px-1 py-0.5 bg-transparent font-bold text-white focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-gray-100 focus:ring-indigo-500"
                aria-expanded="true"
                aria-haspopup="true"
                @click.stop="topTeamSelectShow = !topTeamSelectShow"
              >
                {{ topTeamSelected }}
                <svg
                  v-if="teamThree.length"
                  class="-mr-1 ml-2 h-5 w-5"
                  xmlns="http://www.w3.org/2000/svg"
                  viewBox="0 0 20 20"
                  fill="currentColor"
                  aria-hidden="true"
                >
                  <path
                    fill-rule="evenodd"
                    d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z"
                    clip-rule="evenodd"
                  />
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
              <div
                v-if="topTeamSelectShow"
                v-click-outside="onCloseTopSelect"
                class="z-20 origin-top-right absolute right-0 mt-2 w-56 rounded-md shadow-lg bg-white ring-1 ring-black ring-opacity-5 focus:outline-none"
                role="menu"
                aria-orientation="vertical"
                aria-labelledby="menu-button"
                tabindex="-1"
              >
                <div class="py-1" role="none">
                  <a
                    id="menu-item-0"
                    class="text-gray-700 block px-4 py-2 text-sm"
                    role="button"
                    tabindex="-1"
                    :class="{
                      'text-gray-400 pointer-events-none opacity-50':
                        topTeamSelected === 1 || bottomTeamSelected === 1,
                      'text-green-500': topTeamSelected === 1,
                    }"
                    @click="topTeamSelected = 1"
                    >Tim 1</a
                  >
                  <a
                    id="menu-item-1"
                    class="text-gray-700 block px-4 py-2 text-sm"
                    role="button"
                    tabindex="-1"
                    :class="{
                      'text-red-500 pointer-events-none opacity-50':
                        topTeamSelected === 2 || bottomTeamSelected === 2,
                      'text-green-500': topTeamSelected === 2,
                    }"
                    @click="topTeamSelected = 2"
                    >Tim 2</a
                  >
                  <a
                    id="menu-item-2"
                    class="text-gray-700 block px-4 py-2 text-sm"
                    role="button"
                    tabindex="-1"
                    :class="{
                      'text-red-500 pointer-events-none opacity-50':
                        topTeamSelected === 3 || bottomTeamSelected === 3,
                      'text-green-500': topTeamSelected === 3,
                    }"
                    @click="topTeamSelected = 3"
                    >Tim 3</a
                  >
                </div>
              </div>
            </transition>
          </div>
          <!--          <select id="topTeamSelected" v-model="topTeamSelected" :disabled="!teamThree.length" class="text-black" name="topTeamSelected">-->
          <!--            <option :disabled="topTeamSelected === 1 || bottomTeamSelected === 1" :value="1">1</option>-->
          <!--            <option :disabled="topTeamSelected === 2 || bottomTeamSelected === 2" :value="2">2</option>-->
          <!--            <option v-if="teamThree.length" :disabled="topTeamSelected === 3 || bottomTeamSelected === 3" :value="3">3</option>-->
          <!--          </select>-->
        </div>
        <!--        <ul class="px-4 overflow-y-scroll overflow-x-hidden h-[calc(100%-1.5rem)]">-->
        <!--          <li v-for="n in 8" :key="n">{{n}}. Player</li>-->
        <!--        </ul>-->
        <div
          class="pt-3 grid grid-flow-row-dense grid-cols-6 grid-rows-3 gap-y-2"
        >
          <template v-for="(topTeamPlayer, topTeamPlayerIndex) in topTeam">
            <div
              v-if="topTeamPlayerIndex === 0"
              :key="`${topTeamPlayer.id}-topTeam--1`"
              class="col-span-6 m-auto flex items-center flex-col gap-2"
            >
              <div class="relative">
                <img
                  class="w-10 h-10"
                  :src="
                    require(`@/static/images/player/${topTeamPlayer.id}.png`)
                  "
                  :alt="topTeamPlayer.name"
                />
                <div
                  class="hidden absolute bottom-0 left-0 bg-green-600 py-0.5 px-1 opacity-75 hover:opacity-100 rounded-tr"
                  style="font-size: 7px"
                  v-text="topTeamPlayer.won"
                />
                <div
                  class="hidden absolute bottom-0 right-0 bg-red-600 py-0.5 px-1 opacity-75 hover:opacity-100 rounded-tl"
                  style="font-size: 7px"
                  v-text="topTeamPlayer.lost"
                />
              </div>
              <div
                class="bg-black px-2 py-1 text-xs rounded opacity-80"
                v-text="topTeamPlayer.name"
              />
            </div>
            <div
              v-else-if="topTeamPlayerIndex === 1"
              :key="`${topTeamPlayer.id}-topTeam--2`"
              class="col-span-3 m-auto flex items-center flex-col gap-2"
            >
              <div class="relative">
                <img
                  class="w-10 h-10"
                  :src="
                    require(`@/static/images/player/${topTeamPlayer.id}.png`)
                  "
                  :alt="topTeamPlayer.name"
                />
                <div
                  class="hidden absolute bottom-0 left-0 bg-green-600 py-0.5 px-1 opacity-75 hover:opacity-100 rounded-tr"
                  style="font-size: 7px"
                  v-text="topTeamPlayer.won"
                />
                <div
                  class="hidden absolute bottom-0 right-0 bg-red-600 py-0.5 px-1 opacity-75 hover:opacity-100 rounded-tl"
                  style="font-size: 7px"
                  v-text="topTeamPlayer.lost"
                />
              </div>
              <div
                class="bg-black px-2 py-1 text-xs rounded opacity-80"
                v-text="topTeamPlayer.name"
              />
            </div>
            <div
              v-else-if="topTeamPlayerIndex === 2"
              :key="`${topTeamPlayer.id}-topTeam--3`"
              class="col-span-3 m-auto flex items-center flex-col gap-2"
            >
              <div class="relative">
                <img
                  class="w-10 h-10"
                  :src="
                    require(`@/static/images/player/${topTeamPlayer.id}.png`)
                  "
                  :alt="topTeamPlayer.name"
                />
                <div
                  class="hidden absolute bottom-0 left-0 bg-green-600 py-0.5 px-1 opacity-75 hover:opacity-100 rounded-tr"
                  style="font-size: 7px"
                  v-text="topTeamPlayer.won"
                />
                <div
                  class="hidden absolute bottom-0 right-0 bg-red-600 py-0.5 px-1 opacity-75 hover:opacity-100 rounded-tl"
                  style="font-size: 7px"
                  v-text="topTeamPlayer.lost"
                />
              </div>
              <div
                class="bg-black px-2 py-1 text-xs rounded opacity-80"
                v-text="topTeamPlayer.name"
              />
            </div>
            <div
              v-else-if="topTeamPlayerIndex === 3"
              :key="`${topTeamPlayer.id}-topTeam--4`"
              class="col-span-3 ml-auto pr-8 flex items-center flex-col gap-2"
            >
              <div class="relative">
                <img
                  class="w-10 h-10"
                  :src="
                    require(`@/static/images/player/${topTeamPlayer.id}.png`)
                  "
                  :alt="topTeamPlayer.name"
                />
                <div
                  class="hidden absolute bottom-0 left-0 bg-green-600 py-0.5 px-1 opacity-75 hover:opacity-100 rounded-tr"
                  style="font-size: 7px"
                  v-text="topTeamPlayer.won"
                />
                <div
                  class="hidden absolute bottom-0 right-0 bg-red-600 py-0.5 px-1 opacity-75 hover:opacity-100 rounded-tl"
                  style="font-size: 7px"
                  v-text="topTeamPlayer.lost"
                />
              </div>
              <div
                class="bg-black px-2 py-1 text-xs rounded opacity-80"
                v-text="topTeamPlayer.name"
              />
            </div>
            <div
              v-else-if="topTeamPlayerIndex === 4"
              :key="`${topTeamPlayer.id}-topTeam--5`"
              class="col-span-3 mr-auto pl-8 flex items-center flex-col gap-2"
            >
              <div class="relative">
                <img
                  class="w-10 h-10"
                  :src="
                    require(`@/static/images/player/${topTeamPlayer.id}.png`)
                  "
                  :alt="topTeamPlayer.name"
                />
                <div
                  class="hidden absolute bottom-0 left-0 bg-green-600 py-0.5 px-1 opacity-75 hover:opacity-100 rounded-tr"
                  style="font-size: 7px"
                  v-text="topTeamPlayer.won"
                />
                <div
                  class="hidden absolute bottom-0 right-0 bg-red-600 py-0.5 px-1 opacity-75 hover:opacity-100 rounded-tl"
                  style="font-size: 7px"
                  v-text="topTeamPlayer.lost"
                />
              </div>
              <div
                class="bg-black px-2 py-1 text-xs rounded opacity-80"
                v-text="topTeamPlayer.name"
              />
            </div>
          </template>
        </div>
      </div>
    </div>
    <div class="absolute top-[18.25rem] w-full">
      <div
        class="bg-black bg-opacity-25 text-white w-[21.7rem] h-[16.95rem] m-auto"
      >
        <!--        <ul class="px-4 overflow-y-scroll overflow-x-hidden h-[calc(100%-1.5rem)]">-->
        <!--          <li v-for="n in 8" :key="n">{{n}}. Player</li>-->
        <!--        </ul>-->
        <div
          class="pb-3 pt-1 grid grid-flow-row-dense grid-cols-6 grid-rows-3 gap-y-2"
        >
          <template
            v-for="(bottomTeamPlayer, bottomTeamPlayerIndex) in bottomTeam"
          >
            <div
              v-if="bottomTeamPlayerIndex === 0"
              :key="`${bottomTeamPlayer.id}-bottomTeam--1`"
              class="col-span-3 ml-auto pr-8 flex items-center flex-col gap-2"
            >
              <div
                class="bg-black px-2 py-1 text-xs rounded opacity-80"
                v-text="bottomTeamPlayer.name"
              />
              <div class="relative">
                <img
                  class="w-10 h-10"
                  :src="
                    require(`@/static/images/player/${bottomTeamPlayer.id}.png`)
                  "
                  :alt="bottomTeamPlayer.name"
                />
                <div
                  class="hidden absolute bottom-0 left-0 bg-green-600 py-0.5 px-1 opacity-75 hover:opacity-100 rounded-tr"
                  style="font-size: 7px"
                  v-text="bottomTeamPlayer.won"
                />
                <div
                  class="hidden absolute bottom-0 right-0 bg-red-600 py-0.5 px-1 opacity-75 hover:opacity-100 rounded-tl"
                  style="font-size: 7px"
                  v-text="bottomTeamPlayer.lost"
                />
              </div>
            </div>
            <div
              v-else-if="bottomTeamPlayerIndex === 1"
              :key="`${bottomTeamPlayer.id}-bottomTeam--2`"
              class="col-span-3 mr-auto pl-8 flex items-center flex-col gap-2"
            >
              <div
                class="bg-black px-2 py-1 text-xs rounded opacity-80"
                v-text="bottomTeamPlayer.name"
              />
              <div class="relative">
                <img
                  class="w-10 h-10"
                  :src="
                    require(`@/static/images/player/${bottomTeamPlayer.id}.png`)
                  "
                  :alt="bottomTeamPlayer.name"
                />
                <div
                  class="hidden absolute bottom-0 left-0 bg-green-600 py-0.5 px-1 opacity-75 hover:opacity-100 rounded-tr"
                  style="font-size: 7px"
                  v-text="bottomTeamPlayer.won"
                />
                <div
                  class="hidden absolute bottom-0 right-0 bg-red-600 py-0.5 px-1 opacity-75 hover:opacity-100 rounded-tl"
                  style="font-size: 7px"
                  v-text="bottomTeamPlayer.lost"
                />
              </div>
            </div>
            <div
              v-else-if="bottomTeamPlayerIndex === 2"
              :key="`${bottomTeamPlayer.id}-bottomTeam--3`"
              class="col-span-3 m-auto flex items-center flex-col gap-2"
            >
              <div
                class="bg-black px-2 py-1 text-xs rounded opacity-80"
                v-text="bottomTeamPlayer.name"
              />
              <div class="relative">
                <img
                  class="w-10 h-10"
                  :src="
                    require(`@/static/images/player/${bottomTeamPlayer.id}.png`)
                  "
                  :alt="bottomTeamPlayer.name"
                />
                <div
                  class="hidden absolute bottom-0 left-0 bg-green-600 py-0.5 px-1 opacity-75 hover:opacity-100 rounded-tr"
                  style="font-size: 7px"
                  v-text="bottomTeamPlayer.won"
                />
                <div
                  class="hidden absolute bottom-0 right-0 bg-red-600 py-0.5 px-1 opacity-75 hover:opacity-100 rounded-tl"
                  style="font-size: 7px"
                  v-text="bottomTeamPlayer.lost"
                />
              </div>
            </div>
            <div
              v-else-if="bottomTeamPlayerIndex === 3"
              :key="`${bottomTeamPlayer.id}-bottomTeam--4`"
              class="col-span-3 m-auto flex items-center flex-col gap-2"
            >
              <div
                class="bg-black px-2 py-1 text-xs rounded opacity-80"
                v-text="bottomTeamPlayer.name"
              />
              <div class="relative">
                <img
                  class="w-10 h-10"
                  :src="
                    require(`@/static/images/player/${bottomTeamPlayer.id}.png`)
                  "
                  :alt="bottomTeamPlayer.name"
                />
                <div
                  class="hidden absolute bottom-0 left-0 bg-green-600 py-0.5 px-1 opacity-75 hover:opacity-100 rounded-tr"
                  style="font-size: 7px"
                  v-text="bottomTeamPlayer.won"
                />
                <div
                  class="hidden absolute bottom-0 right-0 bg-red-600 py-0.5 px-1 opacity-75 hover:opacity-100 rounded-tl"
                  style="font-size: 7px"
                  v-text="bottomTeamPlayer.lost"
                />
              </div>
            </div>
            <div
              v-else-if="bottomTeamPlayerIndex === 4"
              :key="`${bottomTeamPlayer.id}-bottomTeam--5`"
              class="col-span-6 m-auto flex items-center flex-col gap-2"
            >
              <div
                class="bg-black px-2 py-1 text-xs rounded opacity-80"
                v-text="bottomTeamPlayer.name"
              />
              <div class="relative">
                <img
                  class="w-10 h-10"
                  :src="
                    require(`@/static/images/player/${bottomTeamPlayer.id}.png`)
                  "
                  :alt="bottomTeamPlayer.name"
                />
                <div
                  class="hidden absolute bottom-0 left-0 bg-green-600 py-0.5 px-1 opacity-75 hover:opacity-100 rounded-tr"
                  style="font-size: 7px"
                  v-text="bottomTeamPlayer.won"
                />
                <div
                  class="hidden absolute bottom-0 right-0 bg-red-600 py-0.5 px-1 opacity-75 hover:opacity-100 rounded-tl"
                  style="font-size: 7px"
                  v-text="bottomTeamPlayer.lost"
                />
              </div>
            </div>
          </template>
        </div>
        <div
          v-if="bottomTeamSelected"
          class="h-6 px-4 font-bold text-center flex items-center justify-center gap-2"
        >
          <h6 class="mb-1">Tim</h6>
          <div
            class="mb-1 relative inline-block text-left"
            :class="{ 'pointer-events-none': !teamThree.length }"
          >
            <div>
              <button
                id="menu-button"
                type="button"
                class="inline-flex justify-center w-full rounded-md border-none px-1 py-0.5 bg-transparent font-bold text-white focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-gray-100 focus:ring-indigo-500"
                aria-expanded="true"
                aria-haspopup="true"
                @click.stop="bottomTeamSelectShow = !bottomTeamSelectShow"
              >
                {{ bottomTeamSelected }}
                <svg
                  v-if="teamThree.length"
                  class="-mr-1 ml-2 h-5 w-5"
                  xmlns="http://www.w3.org/2000/svg"
                  viewBox="0 0 20 20"
                  fill="currentColor"
                  aria-hidden="true"
                >
                  <path
                    fill-rule="evenodd"
                    d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z"
                    clip-rule="evenodd"
                  />
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
              <div
                v-if="bottomTeamSelectShow"
                v-click-outside="onCloseBottomSelect"
                class="z-20 origin-top-right absolute right-0 mt-2 w-56 rounded-md shadow-lg bg-white ring-1 ring-black ring-opacity-5 focus:outline-none"
                role="menu"
                aria-orientation="vertical"
                aria-labelledby="menu-button"
                tabindex="-1"
              >
                <div class="py-1" role="none">
                  <a
                    id="menu-item-0"
                    class="text-gray-700 block px-4 py-2 text-sm"
                    role="button"
                    tabindex="-1"
                    :class="{
                      'text-gray-400 pointer-events-none opacity-50':
                        topTeamSelected === 1 || bottomTeamSelected === 1,
                      'text-green-500': bottomTeamSelected === 1,
                    }"
                    @click="bottomTeamSelected = 1"
                    >Tim 1</a
                  >
                  <a
                    id="menu-item-1"
                    class="text-gray-700 block px-4 py-2 text-sm"
                    role="button"
                    tabindex="-1"
                    :class="{
                      'text-red-500 pointer-events-none opacity-50':
                        topTeamSelected === 2 || bottomTeamSelected === 2,
                      'text-green-500': bottomTeamSelected === 2,
                    }"
                    @click="bottomTeamSelected = 2"
                    >Tim 2</a
                  >
                  <a
                    id="menu-item-2"
                    class="text-gray-700 block px-4 py-2 text-sm"
                    role="button"
                    tabindex="-1"
                    :class="{
                      'text-red-500 pointer-events-none opacity-50':
                        topTeamSelected === 3 || bottomTeamSelected === 3,
                      'text-green-500': bottomTeamSelected === 3,
                    }"
                    @click="bottomTeamSelected = 3"
                    >Tim 3</a
                  >
                </div>
              </div>
            </transition>
          </div>
          <!--          <select id="bottomTeamSelected" v-model="bottomTeamSelected" :disabled="!teamThree.length" class="form-select text-white bg-transparent focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50" name="bottomTeamSelected">-->
          <!--            <option class="text-black" :disabled="topTeamSelected === 1 || bottomTeamSelected === 1" :value="1">1</option>-->
          <!--            <option class="text-black" :disabled="topTeamSelected === 2 || bottomTeamSelected === 2" :value="2">2</option>-->
          <!--            <option v-if="teamThree.length" class="text-black" :disabled="topTeamSelected === 3 || bottomTeamSelected === 3" :value="3">3</option>-->
          <!--          </select>-->
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import cloneDeep from 'lodash/cloneDeep'
import ClickOutside from '~/directives/clickOutside'
export default {
  name: 'ElField',
  directives: {
    ClickOutside,
  },
  props: {
    teamOne: {
      type: Array,
      default: () => [],
    },
    teamTwo: {
      type: Array,
      default: () => [],
    },
    teamThree: {
      type: Array,
      default: () => [],
    },
  },
  data: () => ({
    topTeam: [],
    bottomTeam: [],
    topTeamSelected: 0,
    topTeamSelectShow: false,
    bottomTeamSelected: 0,
    bottomTeamSelectShow: false,
  }),
  watch: {
    topTeamSelected: {
      handler(val) {
        this.selectTopTeam(val)
      },
    },
    bottomTeamSelected: {
      handler(val) {
        this.selectBottomTeam(val)
      },
    },
  },
  mounted() {
    this.initialTeams()
  },
  methods: {
    initialTeams() {
      console.log('this.initialTeams()');
      if (this.teamOne.length) {
        this.topTeam = cloneDeep(this.teamOne.slice(0, 5))
        this.topTeamSelected = 1
      }
      if (this.teamTwo.length) {
        this.bottomTeam = cloneDeep(this.teamTwo.slice(0, 5))
        this.bottomTeamSelected = 2
      }
    },
    selectTopTeam(val) {
      switch (val) {
        case 1:
          this.topTeam = cloneDeep(this.teamOne.slice(0, 5))
          break
        case 2:
          this.topTeam = cloneDeep(this.teamTwo.slice(0, 5))
          break
        case 3:
          this.topTeam = cloneDeep(this.teamThree.slice(0, 5))
          break
      }
    },
    selectBottomTeam(val) {
      switch (val) {
        case 1:
          this.bottomTeam = cloneDeep(this.teamOne.slice(0, 5))
          break
        case 2:
          this.bottomTeam = cloneDeep(this.teamTwo.slice(0, 5))
          break
        case 3:
          this.bottomTeam = cloneDeep(this.teamThree.slice(0, 5))
          break
      }
    },
    onCloseTopSelect() {
      this.topTeamSelectShow = false
    },
    onCloseBottomSelect() {
      this.bottomTeamSelectShow = false
    },
  },
}
</script>
