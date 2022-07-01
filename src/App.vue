<template>
  <div class="container">
    <time-number v-for="(item, index) in time" :key="index" :index="index">
      <template v-slot:label>{{ item.label }}</template>
      {{ item.value }}
    </time-number>
  </div>
</template>

<script>
import TimeNumber from "./components/TimeNumber.vue";

export default {
  components: { TimeNumber },
  name: "App",
  data() {
    return {
      endDate: new Date(),
      currentDate: new Date().getHours,
      time: {
        d: { label: "Days", value: 0 },
        h: { label: "Hours", value: 0 },
        m: { label: "Minutes", value: 0 },
        s: { label: "Seconds", value: 0 },
      },
    };
  },
  mounted() {
    this.getDataBase();
    this.updateDate();
  },
  computed: {
    day() {
      const d = Math.floor(
        (this.endDate - this.currentDate) / (1000 * 60 * 60 * 24)
      );
      if (d <= 0) {
        return "00";
      }
      return d > 9 ? d : "0" + d;
    },
    hour() {
      const h =
        Math.floor((this.endDate - this.currentDate) / (1000 * 60 * 60)) % 24;
      if (h <= 0) {
        return "00";
      }
      return h > 9 ? h : "0" + h;
    },
    minute() {
      const m =
        Math.floor((this.endDate - this.currentDate) / (1000 * 60)) % 60;
      if (m <= 0) {
        return "00";
      }
      return m > 9 ? m : "0" + m;
    },
    second() {
      const s = Math.floor((this.endDate - this.currentDate) / 1000) % 60;
      if (s <= 0) {
        return "00";
      }
      return s > 9 ? s : "0" + s;
    },
  },
  methods: {
    updateDate() {
      this.currentDate = new Date();
      this.time.d.value = this.day;
      this.time.h.value = this.hour;
      this.time.m.value = this.minute;
      this.time.s.value = this.second;
      setTimeout(() => {
        this.updateDate();
        this.getDataBase();
      }, 1000);
    },
    getDataBase() {
      fetch(
        "https://vue-http-project-eb74d-default-rtdb.europe-west1.firebasedatabase.app/EndDate.json"
      )
        .then((result) => {
          return result.json();
        })
        .then((data) => {
          for (const id in data) {
            this.endDate = new Date(data[id].EndDate);
          }
        });
    },
  },
};
</script>

<style>
* {
  margin: 0;
}

@import url("https://fonts.googleapis.com/css2?family=Barlow:ital,wght@0,600;1,500&display=swap");

#app {
  background-image: url("./assets/wp.png");
  background-size: cover;
  width: 100%;
  height: 100vh;
  display: grid;
  align-content: center;
}

.container {
  display: grid;
  width: 37%;
  grid-template-columns: 1fr 0.1fr 1fr 0.1fr 1fr 0.1fr 1fr;
  margin-left: 16%;
}
</style>

