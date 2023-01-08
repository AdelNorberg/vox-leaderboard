<template>
  <div class="leaderboard">
    <div class="header">CLAN WAR</div>
    <div class="not-official">Not official Voxiom.io leaderboard</div>

    <div class="description">
      The last week of BR and CTG of all clan players is taken into account
    </div>

    <div class="list">
      <div v-for="(clan, key) in 100" :key="key" class="clan">
        <div class="place">{{ key + 1 }}</div>
        <div class="tag">AAAA</div>
        <div class="name">Aboba Abob</div>
        <div class="leader">AdelNorberg</div>
        <div class="scores">51 125</div>
      </div>
    </div>

    <img :src="bgSvg" class="img-1" />
    <img :src="bg2Svg" class="img-2" />
    <img :src="bg3Svg" class="img-3" />
  </div>
</template>

<style lang="scss">
@import "normalize.css";
@import url("https://fonts.googleapis.com/css2?family=Kanit:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap");

body,
#app {
  width: 100vw;
  height: 100vh;
  padding: 0;
  margin: 0;
  font-family: "Kanit", sans-serif;
  font-weight: 500;
}
</style>

<style lang="scss" scoped>
.leaderboard {
  width: 100vw;
  height: 100vh;
  background: linear-gradient(97.27deg, #105fa8 5.99%, #009ef8 98.74%);
  color: white;
  position: relative;
}

.header {
  text-shadow: 0px 5.26186px 5.26186px rgba(0, 0, 0, 0.25);
  font-size: 84px;
  font-weight: Bold;
  width: 100%;
  text-align: center;
  padding-top: 50px;
  position: relative;
  z-index: 5;
}

.not-official {
  color: rgba(255, 218, 72, 1);
  position: absolute;
  top: 0;
  left: 0;
  font-size: 24px;
  padding: 20px 0 0 20px;
}

.img-1 {
  position: absolute;
  right: 0;
  bottom: 0;
  z-index: 1;
}

.img-2 {
  position: absolute;
  left: 300px;
  top: 150px;
}

.img-3 {
  position: absolute;
  right: 0;
  bottom: 0;
  z-index: 0;
}

.description {
  font-size: 31px;
  font-weight: Bold;
  text-shadow: 0px 2.63093px 2.63093px rgba(0, 0, 0, 0.25);
  text-align: center;
  position: relative;
  z-index: 2;
  margin-top: 20px;
}

.list {
  width: 1400px;
  height: 856px;
  display: flex;
  flex-wrap: wrap;
  background-color: #0e5a9a;
  position: absolute;
  bottom: 0;
  left: 0;
  overflow-y: auto;
  z-index: 2;

  &::-webkit-scrollbar {
    width: 0.5rem;
    background: rgba(7, 24, 53, 0.5);
  }

  &::-webkit-scrollbar-thumb {
    background: rgba(98, 124, 168, 0.8);
    border-radius: 0.25rem;
  }
}

.clan {
  display: flex;
  justify-content: space-between;
  width: 400px;
  margin-left: 20px;
  background-color: #0e66b1;
  margin-top: 10px;
  height: 39px;
  align-items: center;
  padding: 0 20px;
}

.place {
  text-shadow: 0px 2px 2px rgba(0, 0, 0, 0.25);
  font-size: 24px;
  color: rgba(255, 218, 72, 1);
}
</style>

<script setup>
import "@/assets/global.scss?inline";
import bgSvg from "@/assets/bg.svg";
import bg2Svg from "@/assets/bg2.svg";
import bg3Svg from "@/assets/bg3.svg";

const allClans = { AAAA: { scores: 50000 } };
</script>
