<template>
  <div v-if="posts.length">
    <h3 class="post__title">Список постов</h3>
    <transition-group name="post-list">
      <post-item
        @remove="$emit('remove', post)"
        v-for="post in posts"
        :key="post.id"
        :post="post"
      />
    </transition-group>
  </div>
  <h2 v-else style="color: red">Список постов пуст</h2>
</template>

<script>
import PostItem from "@/components/PostItem";

export default {
  components: { PostItem },
  props: {
    posts: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped>
.post__title {
  margin-top: 20px;
}

.post-list-item {
  display: inline-block;
  margin-right: 10px;
}
.post-list-enter-active,
.post-list-leave-active {
  transition: all 0.3s ease;
}

.post-list-move {
  transition: transform 0.4s ease;
}

.post-list-enter-from,
.post-list-leave-to {
  opacity: 0;
  transform: translateX(130px);
}
</style>