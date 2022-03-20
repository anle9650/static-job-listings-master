<template>
  <header class="mb-2 mb-lg-5"></header>
  <section
    :class="['container', filters.length === 0 ? '' : 'filter-container']"
  >
    <JobFilter
      class="mb-lg-4"
      v-show="filters.length != 0"
      :filters="filters"
      @remove-filter="removeFilter"
      @clear="filters = []"
    />
    <JobCard
      class="mb-lg-3"
      v-for="job in jobs"
      :key="job.id"
      :jobData="job"
      v-show="passesFilter(job)"
      @add-filter="addFilter"
    />

    <div class="attribution mt-5">
      Challenge by
      <a href="https://www.frontendmentor.io?ref=challenge" target="_blank"
        >Frontend Mentor</a
      >. Coded by <a href="#">Andy Le</a>.
    </div>
  </section>
</template>

<script>
import jobData from "./assets/data.json";
import JobFilter from "./components/JobFilter.vue";
import JobCard from "./components/JobCard.vue";

export default {
  name: "App",
  components: {
    JobFilter,
    JobCard,
  },
  data() {
    return {
      jobs: jobData,
      filters: [],
    };
  },
  methods: {
    addFilter(filter) {
      if (!this.filters.includes(filter)) {
        this.filters.push(filter);
      }
    },
    removeFilter(filter) {
      this.filters = this.filters.filter((thisFilter) => thisFilter != filter);
    },
    passesFilter(job) {
      return this.filters.every((filter) =>
        [job.role, job.level, ...job.languages].includes(filter)
      );
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Spartan:wght@500;700&display=swap");

body {
  background-color: hsl(180, 52%, 96%);
  font-family: "Spartan", sans-serif;
  font-size: 15px;
}
header {
  background-image: url("./assets/bg-header-mobile.svg");
  background-size: cover;
  background-color: hsl(180, 29%, 50%);
  height: 25vh;
}
.filter-container {
  position: absolute;
  top: 21.5vh;
  left: 50%;
  transform: translateX(-50%);
}

.badge.bg-primary {
  color: hsl(180, 29%, 50%);
  background-color: hsl(180, 52%, 96%) !important;
}

.attribution {
  font-size: 11px;
  text-align: center;
}
.attribution a {
  color: hsl(228, 45%, 44%);
}

@media screen and (min-width: 992px) {
  header {
    background-image: url("./assets/bg-header-desktop.svg");
  }
}
</style>
