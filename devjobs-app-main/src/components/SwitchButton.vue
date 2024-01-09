<template>
  <label for="switch" class="switch">
    <input type="checkbox" id="switch" :checked="checkedTheme" @click="toggleTheme" />
    <span class="slider"></span>
  </label>
</template>

<script>
export default {
  data() {
    return {
      checkedTheme: false
    };
  },
  methods: {
    toggleTheme() {
      this.checkedTheme = !this.checkedTheme;
      this.$store.commit("TOGGLE_THEME");
    }
  }
};
</script>

