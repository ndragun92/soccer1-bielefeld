<template>
  <div class="w-full h-full">
    <img class="w-96 m-auto" src="/images/football_field.svg" alt="">
    <div class="absolute top-[1.1rem] w-full">
      <div class="bg-black bg-opacity-25 text-white w-[21.7rem] h-[16.95rem] m-auto">
        <h6 class="h-6 px-4 font-bold text-center">Team 1</h6>
<!--        <ul class="px-4 overflow-y-scroll overflow-x-hidden h-[calc(100%-1.5rem)]">-->
<!--          <li v-for="n in 8" :key="n">{{n}}. Player</li>-->
<!--        </ul>-->
        <div class="pt-3 grid grid-flow-row-dense grid-cols-6 grid-rows-3 gap-y-2">
          <div class="col-span-6 m-auto flex items-center flex-col gap-2">
            <img class="w-10 h-10" src="/images/player/1.png" alt="">
            <div class="bg-black px-2 py-1 text-xs">Player 1</div>
          </div>
          <div class="col-span-3 m-auto flex items-center flex-col gap-2">
            <img class="w-10 h-10" src="/images/player/2.png" alt="">
            <div class="bg-black px-2 py-1 text-xs">Player 2</div>
          </div>
          <div class="col-span-3 m-auto flex items-center flex-col gap-2">
            <img class="w-10 h-10" src="/images/player/3.png" alt="">
            <div class="bg-black px-2 py-1 text-xs">Player 3</div>
          </div>
          <div class="col-span-3 ml-auto pr-8 flex items-center flex-col gap-2">
            <img class="w-10 h-10" src="/images/player/4.png" alt="">
            <div class="bg-black px-2 py-1 text-xs">Player 4</div>
          </div>
          <div class="col-span-3 mr-auto pl-8 flex items-center flex-col gap-2">
            <img class="w-10 h-10" src="/images/player/5.png" alt="">
            <div class="bg-black px-2 py-1 text-xs">Player 5</div>
          </div>
        </div>
      </div>
    </div>
    <div class="absolute top-[18.25rem] w-full">
      <div class="bg-black bg-opacity-25 text-white w-[21.7rem] h-[16.95rem] m-auto">
<!--        <ul class="px-4 overflow-y-scroll overflow-x-hidden h-[calc(100%-1.5rem)]">-->
<!--          <li v-for="n in 8" :key="n">{{n}}. Player</li>-->
<!--        </ul>-->
        <div class="pt-3 grid grid-flow-row-dense grid-cols-6 grid-rows-3 gap-y-2">
          <div class="col-span-3 ml-auto pr-8 flex items-center flex-col gap-2">
            <div class="bg-black px-2 py-1 text-xs">Player 5</div>
            <img class="w-10 h-10" src="/images/player/10.png" alt="">
          </div>
          <div class="col-span-3 mr-auto pl-8 flex items-center flex-col gap-2">
            <div class="bg-black px-2 py-1 text-xs">Player 4</div>
            <img class="w-10 h-10" src="/images/player/9.png" alt="">
          </div>
          <div class="col-span-3 m-auto flex items-center flex-col gap-2">
            <div class="bg-black px-2 py-1 text-xs">Player 3</div>
            <img class="w-10 h-10" src="/images/player/8.png" alt="">
          </div>
          <div class="col-span-3 m-auto flex items-center flex-col gap-2">
            <div class="bg-black px-2 py-1 text-xs">Player 2</div>
            <img class="w-10 h-10" src="/images/player/7.png" alt="">
          </div>
          <div class="col-span-6 m-auto flex items-center flex-col gap-2">
            <div class="bg-black px-2 py-1 text-xs">Player 1</div>
            <img class="w-10 h-10" src="/images/player/6.png" alt="">
          </div>
        </div>
        <h6 class="h-6 px-4 font-bold text-center">Team 2</h6>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ElField',
}
</script>
