<template>
  <div class="digit">
    <p class="label"><slot name="label"></slot></p>
    <p class="number"><slot></slot></p>
  </div>
  <div class="sepparator" v-if="index !== 's'">
    <p>:</p>
  </div>
</template>

<script>
export default {
  props: ["index"],
};
</script>

<style scoped>
.digit {
  display: grid;
  text-align: center;
  font-size: 4rem;
  grid-template-rows: 0.5fr 2fr;
}
.label {
  color: #142b44;
  font-family: "Barlow", sans-serif;
  font-weight: 500;
  font-size: 1.563rem;
}
.number {
  font-size: 5.938rem;
  font-family: "Barlow", sans-serif;
  font-weight: 600;
  color: #142b44;
}
.sepparator {
  font-size: 5.938rem;
  font-family: "Barlow", sans-serif;
  font-weight: 600;
  color: #142b44;
  display: grid;
  grid-template-rows: 0.5fr 2fr;
}
.sepparator p {
  grid-row-start: 2;
}
</style>
