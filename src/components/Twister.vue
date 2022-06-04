<template>
  <div class="twister-panel">
    <p class="instruction">{{ side }} {{ limb }} on {{ color }}</p>
    <div
      class="limb-wrapper"
      :class="[side, color]"
      :style="{ backgroundColor: color }"
    >
      <svg class="limb" v-if="limb === 'hand'" viewBox="0 0 24 24">
        <path
          fill="currentColor"
          d="M3 16V5.75C3 5.06 3.56 4.5 4.25 4.5S5.5 5.06 5.5 5.75V12H6.5V2.75C6.5 2.06 7.06 1.5 7.75 1.5C8.44 1.5 9 2.06 9 2.75V12H10V1.25C10 .56 10.56 0 11.25 0S12.5 .56 12.5 1.25V12H13.5V3.25C13.5 2.56 14.06 2 14.75 2S16 2.56 16 3.25V15H16.75L18.16 11.47C18.38 10.92 18.84 10.5 19.4 10.31L20.19 10.05C21 9.79 21.74 10.58 21.43 11.37L18.4 19C17.19 22 14.26 24 11 24C6.58 24 3 20.42 3 16Z"
        />
      </svg>
      <svg class="limb" v-else viewBox="0 0 24 24">
        <path
          fill="currentColor"
          d="M16 2A2 2 0 1 1 14 4A2 2 0 0 1 16 2M12.04 3A1.5 1.5 0 1 1 10.54 4.5A1.5 1.5 0 0 1 12.04 3M9.09 4.5A1 1 0 1 1 8.09 5.5A1 1 0 0 1 9.09 4.5M7.04 6A1 1 0 1 1 6.04 7A1 1 0 0 1 7.04 6M14.53 12A2.5 2.5 0 0 0 17 9.24A2.6 2.6 0 0 0 14.39 7H11.91A6 6 0 0 0 6.12 11.4A2 2 0 0 0 6.23 12.8A6.8 6.8 0 0 1 6.91 15.76A6.89 6.89 0 0 1 6.22 18.55A1.92 1.92 0 0 0 6.3 20.31A3.62 3.62 0 0 0 10.19 21.91A3.5 3.5 0 0 0 12.36 16.63A2.82 2.82 0 0 1 11.91 15S11.68 12 14.53 12Z"
        />
      </svg>
    </div>
    <button @click="twist">Twist again</button>
  </div>
</template>
<script setup>
import { ref, onMounted } from "vue";
const limb = ref("none");
const side = ref("none");
const color = ref("none");
onMounted(() => {
  twist();
  console.log("mounted");
});
const randomItem = (list) => {
  return list.at(Math.floor(Math.random() * list.length));
};
const twist = () => {
  limb.value = randomItem(["hand", "foot"]);
  side.value = randomItem(["left", "right"]);
  color.value = randomItem([
    "red",
    "green",
    "blue",
    "black",
    "yellow",
    "pink",
    "orange",
  ]);
};
</script>
<style lang="scss" scoped>
.twister-panel {
  width: 256px;
  margin: 0 auto;
  .instruction {
    text-transform: capitalize;
    margin-bottom: 1rem;
  }
  .limb-wrapper {
    margin-bottom: 1rem;
    background-color: #ccc;
    border-radius: 100%;
    width: 256px;
    height: 256px;
    color: #ccc;
    display: flex;
    align-items: center;
    justify-content: center;
    &.yellow,
    &.pink {
      color: #333;
    }
    &.right {
      transform: scaleX(-1);
    }
    .limb {
      width: 128px;
      height: 128px;
    }
  }
}
</style>
