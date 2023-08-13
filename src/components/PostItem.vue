<template>
  <div class="post">
    <div class="post__content">
      <div>№:{{ post.id }}</div>
      <div><strong>Название:</strong> {{ post.title }}</div>
      <div><strong>Описание:</strong> {{ post.body }}</div>
    </div>
    <div class="post__btns">
      <my-button
        class="open-modal__btn"
        @click="$router.push(`/posts/${post.id}`)"
        >Открыть</my-button
      >
      <my-button @click="$emit('remove', post)" class="delete__button"
        >Удалить</my-button
      >
    </div>
  </div>
</template>

<script>
export default {
  props: {
    post: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style scoped>
.post {
  padding: 15px;
  border: 2px solid teal;
  margin-top: 15px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.delete__button {
  border: 2px solid red;
  color: red;
}

.post__btns {
  display: flex;
}

.open-modal__btn {
  margin-right: 20px;
}

.delete__button:hover {
  background-color: red;
}

.post__content {
  gap: 7px;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: start;
}

@media (max-width: 600px) {
  .post {
    flex-direction: column;
  }
  .post__btns {
    margin-top: 15px;
  }
}
</style>