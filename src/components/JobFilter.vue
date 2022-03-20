<template>
  <div class="card shadow">
    <div class="card-body pb-0 px-lg-4">
      <div class="d-flex align-items-center">
        <div class="d-flex flex-wrap me-auto">
          <span
            v-for="filter in filters"
            :key="filter"
            class="badge bg-primary p-0 ps-2 me-3 mb-3"
            >{{ filter }}
            <button
              class="btn btn-sm py-1 ms-1"
              @click="$emit('remove-filter', filter)"
            >
              <img src="../assets/icon-remove.svg" />
            </button>
          </span>
        </div>
        <button
          class="btn btn-clear btn-sm text-muted fw-bold align-self-lg-start"
          @click="$emit('clear')"
        >
          Clear
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "JobFilter",
  props: {
    filters: Array,
  },
  emits: ["remove-filter", "clear"],
};
</script>

<style scoped>
.badge .btn {
  background-color: hsl(180, 29%, 50%);
  border-top-left-radius: 0;
  border-bottom-left-radius: 0;
}
.badge .btn:hover {
  background-color: black;
}
.btn.btn-clear:hover {
  color: hsl(180, 29%, 50%) !important;
  text-decoration: underline;
}
</style>