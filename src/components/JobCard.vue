<template>
  <div>
    <img
      class="logo d-lg-none"
      :src="require('../assets/' + jobData.logo)"
      alt="logo"
    />
    <div :class="['card shadow p-2 pt-3', jobData.featured ? 'featured' : '']">
      <div class="d-lg-flex align-items-center">
        <img
          class="d-none d-lg-block my-3 ms-3"
          :src="require('../assets/' + jobData.logo)"
          alt="logo"
        />
        <div class="card-body pb-0 pt-lg-0">
          <span class="company-text me-3">{{ jobData.company }}</span>
          <span
            v-if="jobData.new"
            class="badge rounded-pill bg-primary px-2 pt-2 me-2"
            >New!</span
          >
          <span
            v-if="jobData.featured"
            class="badge rounded-pill bg-secondary px-2 pt-2"
            >Featured</span
          >
          <h6 class="card-title fw-bold my-3 my-lg-2">
            {{ jobData.position }}
          </h6>
          <span class="card-text text-muted"
            >{{ jobData.postedAt }} <span class="fw-bold mx-lg-2">&#183; </span
            >{{ jobData.contract }} <span class="fw-bold mx-lg-2">&#183; </span
            >{{ jobData.location }}</span
          >
        </div>
        <hr class="d-lg-none" />
        <div class="card-body py-0">
          <div class="d-flex flex-wrap justify-content-lg-end">
            <!-- Role -->
            <span
              class="btn badge bg-primary py-2 me-3 mb-3"
              @click="$emit('add-filter', jobData.role)"
              >{{ jobData.role }}</span
            >
            <!-- Level -->
            <span
              class="btn badge bg-primary py-2 me-3 mb-3"
              @click="$emit('add-filter', jobData.level)"
              >{{ jobData.level }}</span
            >
            <!-- Languages -->
            <span
              class="btn badge bg-primary py-2 me-3 mb-3"
              v-for="language in jobData.languages"
              :key="language"
              @click="$emit('add-filter', language)"
              >{{ language }}</span
            >
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "JobCard",
  props: {
    jobData: Object,
  },
  emits: ["add-filter"],
};
</script>

<style scoped>
img.logo {
  width: 3rem;
  position: relative;
  left: 2rem;
  transform: translateY(50%);
  z-index: 1;
}
.card-title:hover {
  color: hsl(180, 29%, 50%);
  cursor: pointer;
}
.card.featured {
  border-left-color: hsl(180, 29%, 50%);
  border-left-width: thick;
}
.company-text {
  color: hsl(180, 29%, 50%);
  font-weight: 700;
}
.badge.rounded-pill {
  color: white;
  text-transform: uppercase;
}
.badge.rounded-pill.bg-primary {
  background-color: hsl(180, 29%, 50%) !important;
}
.badge.rounded-pill.bg-secondary {
  background-color: hsl(180, 14%, 20%) !important;
}
.btn.badge:hover {
  background-color: hsl(180, 29%, 50%) !important;
  color: white;
}

@media screen and (min-width: 992px) {
  .card-text {
    font-size: 0.8rem;
  }
}
</style>