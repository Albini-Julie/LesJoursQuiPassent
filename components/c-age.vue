<template>
  <div>
    <p class="text">
      <span class="text__number">{{ elapsedTime.years }}</span> ans
    </p>
  </div>
</template>

<script>
export default {
  props: {
    day: Number,
    month: Number,
    year: Number,
    couleur: String,
  },
  data() {
    return {
      elapsedTime: {
        years: 0,
        months: 0,
        days: 0,
        hours: 0,
        minutes: 0,
        seconds: 0,
      },
    };
  },
  methods: {
    calculateTimeElapsed() {
      const selectedDay = parseInt(this.day);
      const selectedMonth = parseInt(this.month);
      const selectedYear = parseInt(this.year);

      const selectedDate = new Date(selectedYear, selectedMonth - 1, selectedDay);
      const currentDate = new Date();

      const elapsedMilliseconds = currentDate - selectedDate;
      const elapsedSeconds = Math.floor(elapsedMilliseconds / 1000);
      const elapsedMinutes = Math.floor(elapsedSeconds / 60);
      const elapsedHours = Math.floor(elapsedMinutes / 60);
      const elapsedDays = Math.floor(elapsedHours / 24);
      const elapsedMonths = Math.floor(elapsedDays / 30.44);
      const elapsedYears = Math.floor(elapsedMonths / 12);

      const remainingMonths = elapsedMonths % 12;
      const remainingDays = Math.floor(elapsedDays % 30.44);
      const remainingHours = Math.floor(elapsedHours % 24);
      const remainingMinutes = Math.floor(elapsedMinutes % 60);
      const remainingSeconds = Math.floor(elapsedSeconds % 60);

      this.elapsedTime = {
        years: elapsedYears,
        months: remainingMonths,
        days: remainingDays,
        hours: remainingHours,
        minutes: remainingMinutes,
        seconds: remainingSeconds,
      };
    },
    formatTimeElapsed() {
      let result = "";

      if (this.elapsedTime.years > 0) {
        result += `${this.elapsedTime.years} an${this.elapsedTime.years === 1 ? "" : "s"}`;
      }

      if (this.elapsedTime.months > 0) {
        result += `${this.elapsedTime.months} mois`;
      }

      if (this.elapsedTime.days > 0) {
        result += `${this.elapsedTime.days} jour${this.elapsedTime.days === 1 ? "" : "s"}`;
      }

      if (this.elapsedTime.hours > 0) {
        result += `${this.elapsedTime.hours} heure${this.elapsedTime.hours === 1 ? "" : "s"}`;
      }

      if (this.elapsedTime.minutes > 0) {
        result += `${this.elapsedTime.minutes} minute${this.elapsedTime.minutes === 1 ? "" : "s"}`;
      }

      if (this.elapsedTime.seconds > 0 || result === "") {
        result += `${this.elapsedTime.seconds} seconde${this.elapsedTime.seconds === 1 ? "" : "s"}`;
      }

      return result;
    },
  },
  mounted() {
    this.calculateTimeElapsed();
    this.timer = setInterval(() => {
      this.calculateTimeElapsed();
    }, 1000);
  },
  beforeDestroy() {
    clearInterval(this.timer);
  },
};
</script>

<style lang="scss" scoped>
.text {
  color: v-bind(couleur);
  font-family: $secondary-font-family;
  font-size: $big-font-size;

  &__number {
    font-size: $giant-font-size;
  }
}
</style>
