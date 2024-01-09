<template>
  <form :class="$store.state.darkTheme ? 'search-form dark' : 'search-form'" @submit.prevent="searchJob">
    <div class="flex-container">
      <div class="search-form__item" id="title">
        <img
          src="@/assets/images/desktop/icon-search.svg"
          alt="search by title"
        />
        <input
          type="text"
          :placeholder="
            screenWidth < 915
              ? 'Filter by title...'
              : 'Filter by title, companies, expertise...'
          "
          :class="$store.state.darkTheme ? 'search-input dark' : 'search-input'"
          v-model="jobQuery"
        />
      </div>
      <div class="search-form__item" id="location">
        <img
          src="@/assets/images/desktop/icon-location.svg"
          alt="search by location"
        />
        <input
          type="text"
          placeholder="Filter by location..."
          :class="$store.state.darkTheme ? 'search-input dark' : 'search-input'"
          v-model="locationQuery"
        />
      </div>
      <div class="search-form__item" id="search">
        <input type="checkbox" class="mr-0-5" id="checkbox" v-model="checked" />
        <label
          for="checkbox"
          :class="$store.state.darkTheme ? 'label-dark' : ''"
        >
          <span v-if="screenWidth > 992">Full Time Only</span>
          <span v-else>Full Time</span>
        </label>
        <button type="submit" class="apply-btn" @click="searchJob">
          Search
        </button>
      </div>
    </div>
  </form>
</template>
<script>
import { mapState } from "vuex";

export default {
  data() {
    return {
      checked: false,
      locationQuery: "",
      jobQuery: "",
      screenWidth: window.innerWidth
    };
  },
  computed: {
    ...mapState({
      darkTheme: state => state.darkTheme
    })
  },
  methods: {
    resetSettings() {
      this.locationQuery = "";
      this.jobQuery = "";
      this.checked = false;
    },
    hasJobQuery() {
      return this.jobQuery.trim() !== "";
    },
    hasLocationQuery() {
      return this.locationQuery !== "";
    },
    isFormValid() {
      return this.hasJobQuery() !== this.hasLocationQuery();
    },
    searchJob(event) {
      event.preventDefault();
      if (!this.isFormValid()) {
        return;
      }
      const filterAction = this.hasJobQuery() ? "filterByTitle" : "filterByLocation";
      const payload = this.hasJobQuery()
        ? { jobQuery: this.jobQuery.trim(), checked: this.checked }
        : { locationQuery: this.locationQuery.trim(), checked: this.checked };

      this.$store.dispatch(filterAction, payload);
      this.resetSettings();
    },
    handleResize() {
      this.screenWidth = window.innerWidth;
    }
  },
  mounted() {
    window.addEventListener("resize", this.handleResize);
  },
  beforeDestroy() {
    window.removeEventListener("resize", this.handleResize);
  }
};
</script>
