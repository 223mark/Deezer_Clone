<template>
  <div class="max-w-[1500px] mx-auto" id="HeaderSection">
    <div class="flex items-center w-full relative h-full px-8 mt-6 min-w-[650px]">
      <img :src="artist.albumCover" width="175" class="rounded-full" alt="" />

      <div class="ml-8">
        <div
          class="text-white text-3xl w-full hover:underline cursor-pointer font-semibold"
        >
          {{ artist.name }}
        </div>
        <div class="text-[#bfbfbf] text-[12px] py-1.5 font-light">167, 026 fans</div>

        <div class="flex gap-4 items-center justify-start bottom-1 mb-1.5">
          <button class="p-2.5 px-6 rounded-full bg-[#EF5465]" @click="playFunc()">
            <div class="flex items-center" v-if="!isPlaying">
              <Play fillColor="#FFFFFF" :size="20" />
              <div class="text-white font-bold text-xs pr-1">PLAY</div>
            </div>
            <div class="flex items-center" v-else>
              <Pause fillColor="#FFFFFF" :size="20" />
              <div class="text-white font-bold text-xs pr-1">PAUSE</div>
            </div>
          </button>
          <button class="rounded-full p-2 border border-[#52525D] hover:bg-[#2b2b30]">
            <HeartOutline fillColor="#EAEAEA" :size="20" />
          </button>
          <button class="rounded-full p-2 border border-[#52525D] hover:bg-[#2b2b30]">
            <DotsHorizontal fillColor="#EAEAEA" :size="20" />
          </button>
        </div>
      </div>
    </div>

    <div class="mt-11">
      <div class="flex justify-between pt-2 min-w-[650px]">
        <ul class="flex items-center justify-start w-full text-gray-400 h-9">
          <li class="pl-8">
            <button
              class="font-light cursor-pointer text-[#bebebe] border-b-2 border-b-[#121216] hover:border-[#FFFFFF] pb-[8px] hover:text-[#FFFFFF]"
            >
              Discography
            </button>
          </li>
          <li class="text-[#FFFFFF] pl-10">
            <button
              class="font-semibold cursor-pointer border-b-2 border-[#EF5465] pb-[8px]"
            >
              Top Tracks
            </button>
          </li>
          <li class="pl-10">
            <button
              class="font-light cursor-pointer text-[#bebebe] border-b-2 border-b-[#121216] hover:border-[#FFFFFF] pb-[8px] hover:text-[#FFFFFF]"
            >
              Similar Artists
            </button>
          </li>
          <li class="pl-10">
            <button
              class="font-light cursor-pointer text-[#bebebe] border-b-2 border-b-[#121216] hover:border-[#FFFFFF] pb-[8px] hover:text-[#FFFFFF]"
            >
              Playlist
            </button>
          </li>
          <li class="pl-10">
            <button
              class="font-light cursor-pointer text-[#bebebe] border-b-2 border-b-[#121216] hover:border-[#FFFFFF] pb-[8px] hover:text-[#FFFFFF]"
            >
              Bio
            </button>
          </li>
        </ul>
      </div>
    </div>
  </div>

  <div class="border-b border-[#302d2d]"></div>
  <div class="mb-10"></div>

  <div class="max-w-[1500px] mx-auto">
    <div class="pl-8">
      <div class="text-white text-2xl font-semibold mb-7">Top Tracks</div>

      <div
        class="flex items-center border border-[#525254] bg-[#23232D] rounded-sm text-[#c9c9c9] w-[300px]"
      >
        <Magnify fillColor="#9B9BA1" class="px-1" />
        <input
          type="text"
          class="w-full py-[5px] bg-[#23232D] text-sm placeholder-[#7e7e7e] outline-none ring-0 hover:ring-0"
          placeholder="Search within tracks"
        />
      </div>
    </div>
    <div class="mb-4"></div>

    <div
      class="flex items-center justify-between min-w-[590px] mx-8 border-b border-b-[#302d2d] py-2.5 px-1.5"
    >
      <div class="text-xs font-light text-[#aeaeae]">TRACK</div>
      <ClockTimeFiveOutline fillColor="#aeaeae" :size="20" />
    </div>

    <ul
      class="w-full mx-8 pr-16 min-w-[650px]"
      v-for="track in artist.tracks"
      :key="track"
    >
      <SongRow v-if="track" :track="track" />
    </ul>
  </div>
  <div class="mb-40"></div>
</template>
<script setup>
//icons
import Magnify from "vue-material-design-icons/Magnify.vue";
import Play from "vue-material-design-icons/Play.vue";
import Pause from "vue-material-design-icons/Pause.vue";
import DotsHorizontal from "vue-material-design-icons/DotsHorizontal.vue";
import HeartOutline from "vue-material-design-icons/HeartOutline.vue";
import ClockTimeFiveOutline from "vue-material-design-icons/ClockTimeFiveOutline.vue";

import artist from "../artist.json";

import SongRow from "../components/SongRow.vue";
//pinia
import { useSongStore } from "../stores/song";
import { storeToRefs } from "pinia";
const useSong = useSongStore();
const { isPlaying, currentTrack, currentArtist } = storeToRefs(useSong);

//funcs

const playFunc = () => {
  if (currentTrack) {
    useSong.playOrPauseThisSong(currentArtist.value, currentTrack.value);
    return;
  }
  useSong.playFromFirst();
};
</script>
