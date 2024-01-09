<template>
  <section class="home-page">
    <div class="container">
      <SearchForm />
      <div class="home-page__columns grid-container">
        <Card
          :jobInformation="job"
          v-for="job in filteredJobs.slice(0, currentAmountOfCards) || job in data"
          :key="job.id"
          @click="setCurrentOffer(job)"
        />
      </div>

      <div v-if="currentAmountOfCards != 13" class="load-more-btn">
        <button @click="increaseAmountOfCards" class="apply-btn">
          Load More
        </button>
      </div>
    </div>
  </section>
</template>

<script>
import Card from "@/components/Card.vue";
import SearchForm from "@/components/SearchForm.vue";
import { mapState, mapMutations } from "vuex";

export default {
  components: { Card, SearchForm },
  data() {
    return {
      currentAmountOfCards: 9
    };
  },
  computed: {
    ...mapState({
      data: state => state.data,
      filteredJobs: state => state.filteredJobs
    })
  },
  methods: {
    ...mapMutations(['SET_CURRENT_OFFER']),
    increaseAmountOfCards() {
      this.currentAmountOfCards = 13;
    },
    setCurrentOffer(job) {
      this.SET_CURRENT_OFFER(job);
    }
  },
  mounted() {
    this.filteredJobs = this.data;
  }
};
</script>
