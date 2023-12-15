<template>
  <div>
    <p class="text">
      <span class="text --number">{{ age }}</span> ans
    </p>
  </div>
</template>

<script>
export default {
  props: {
    couleur: String,
    birthYear: {
      type: Number,
      required: true,
    },
    birthMonth: {
      type: Number,
      required: true,
    },
  },
  data() {
    return {
      currentYear: new Date().getFullYear(),
      currentMonth: new Date().getMonth(),
      age: 0,
    };
  },
  computed: {
    calculateAge() {
      const monthDifference = this.currentMonth - this.birthMonth;
      const age = this.currentYear - this.birthYear;

      return monthDifference < 0 ? age - 1 : age;
    },
  },
  watch: {
    birthYear: "updateAge",
    birthMonth: "updateAge",
    currentYear: "updateAge",
    currentMonth: "updateAge",
  },
  methods: {
    updateAge() {
      this.age = this.calculateAge;
    },
  },
  mounted() {
    this.updateAge();
  },
};
</script>

<style lang="scss" scoped>
.text {
  color: v-bind(couleur);
  font-family: $secondary-font-family;
  font-size: $big-font-size;

  &.--number {
    font-size: $giant-font-size;
  }
}
</style>
