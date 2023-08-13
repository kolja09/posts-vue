<template>
  <div class="page__wrapper">
    <div
      v-for="pageNumber in totalPages"
      :key="pageNumber"
      class="page"
      @click="$emit('changePage', pageNumber)"
      :class="{ 'current-page': page === pageNumber }"
    >
      {{ pageNumber }}
    </div>
  </div>
</template>

<script>
export default {
  props: {
    totalPages: {
      type: Number,
      required: true,
    },
    page: {
      type: Number,
      required: true,
    },
  },
};
</script>

<style scoped>
.page__wrapper {
  display: flex;
  justify-content: center;
  margin-top: 15px;
}

.page {
  border: 1px solid black;
  padding: 10px;
  cursor: pointer;
  margin: 2px;
}

.current-page {
  border: 2px solid green;
}

@media (max-width: 600px) {
  .page {
    padding: 7px;
  }
}
</style>