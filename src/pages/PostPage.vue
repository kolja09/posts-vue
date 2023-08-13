<template>
  <div>
    <h1 class="title">Страница с постами</h1>
    <my-input
      :model-value="searchValue"
      @update:model-value="setSearchValue"
      v-focus
      placeholder="Поиск..."
    />
    <div class="app__buttons">
      <my-button @click="showDialog">Создать пост</my-button>
      <my-select
        :model-value="selectedSort"
        @update:model-value="setSelectedSort"
        :options="sortOptions"
      />
    </div>
    <my-dialog v-model:show="dialogVisible">
      <post-form @create="createPost" />
    </my-dialog>

    <post-list
      v-if="!isLoading"
      :posts="sortedAndSearchedPosts"
      @remove="removePost"
    />
    <div v-else>Loading...</div>

    <my-pagination
      @changePage="changePage"
      :page="page"
      :totalPages="totalPages"
    />
  </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import MyPagination from "@/components/MyPagination";

import { mapState, mapGetters, mapActions, mapMutations } from "vuex";

export default {
  components: {
    PostList,
    PostForm,
    MyPagination,
  },
  data() {
    return {
      dialogVisible: false,
    };
  },
  methods: {
    ...mapMutations({
      setPage: "post/setPage",
      setSearchValue: "post/setSearchValue",
      setSelectedSort: "post/setSelectedSort",
      setPosts: "post/setPosts",
    }),
    ...mapActions({
      fetchPosts: "post/fetchPosts",
    }),
    createPost(post) {
      this.posts.unshift(post);
      this.dialogVisible = false;
    },
    removePost(post) {
      this.setPosts(this.posts.filter((p) => p.id !== post.id));
    },
    showDialog() {
      this.dialogVisible = true;
    },
    changePage(pageNumber) {
      this.setPage(pageNumber);
    },
  },
  mounted() {
    this.fetchPosts();
  },
  watch: {
    page() {
      this.fetchPosts();
    },
  },
  computed: {
    ...mapState({
      posts: (state) => state.post.posts,
      isPostLoading: (state) => state.post.isPostLoading,
      selectedSort: (state) => state.post.selectedSort,
      page: (state) => state.post.page,
      limit: (state) => state.post.limit,
      totalPages: (state) => state.post.totalPages,
      searchValue: (state) => state.post.searchValue,
      sortOptions: (state) => state.post.sortOptions,
    }),
    ...mapGetters({
      sortedPost: "post/sortedPosts",
      sortedAndSearchedPosts: "post/sortedAndSearchedPosts",
    }),
  },
};
</script>

<style>
.title {
  margin-bottom: 20px;
}

.app__buttons {
  display: flex;
  justify-content: space-between;
}
</style>
