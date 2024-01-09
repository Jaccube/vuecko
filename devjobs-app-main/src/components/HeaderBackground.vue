<template>
  <div class="header">
    <header class="main-header">
      <div class="flex-container container">
        <h3 @click="reloadPage" class="main-header__heading">devjobs</h3>
        <div class="theme-switch">
          <img src="@/assets/images/desktop/icon-sun.svg" alt="light theme" />
          <SwitchButton />
          <img src="@/assets/images/desktop/icon-moon.svg" alt="dark theme" />
        </div>
      </div>
    </header>
  </div>
</template>

<script>
import SwitchButton from "@/components/SwitchButton.vue";

export default {
  components: { SwitchButton },
  methods: {
    reloadPage() {
      this.$router.push({ name: "home" });
    }
  }
};
</script>
