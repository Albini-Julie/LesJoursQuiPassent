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
  },
  data() {
    return {
      currentYear: new Date().getFullYear(),
      age: 0,
    };
  },
  computed: {
    calculateAge() {
      return this.currentYear - this.birthYear;
    },
  },
  watch: {
    birthYear: "updateAge",
    currentYear: "updateAge",
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
