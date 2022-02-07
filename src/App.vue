<template>
  <div class="container mx-auto flex flex-col items-center bg-gray-100 p-4">
    <div class="container">
      <section>
        <div class="flex">
          <div class="mr-10">
            <label for="wallet" class="block text-sm font-medium text-gray-700"
              >Search</label
            >
            <div class="mt-1 relative rounded-md shadow-md">
              <input
                v-model="search"
                class="
                  shadow
                  appearance-none
                  border
                  rounded
                  w-full
                  py-2
                  px-3
                  text-gray-700
                  leading-tight
                  focus:outline-none focus:shadow-outline
                "
                id="search"
                type="text"
                placeholder="example ipsam ..."
              />
            </div>
          </div>
        </div>
      </section>

      <hr class="w-full border-t border-gray-600 my-4" />
      <dl class="mt-5 grid grid-cols-1 gap-5 sm:grid-cols-3">
        <Card
          class="
            p-4
            bg-white
            rounded-lg
            border
            shadow-md
            sm:p-6
            dark:bg-gray-800 dark:border-gray-700
          "
          v-for="(post, index) in searchedPosts"
          :key="post.id"
          :post="post"
          :form="form"
          :index="index"
          @saveChanges="saveChanges(post, form[post.id])"
          @disableChanges="disableChanges(post, form[post.id])"
          @handleDelete="handleDelete(post, form[post.id])"
        />
      </dl>
    </div>
  </div>
</template>

<script>
import Card from "@/components/Card";
export default {
  name: "App",
  components: {
    Card,
  },
  data() {
    return {
      posts: [],
      form: [],
      search: "",
    };
  },
  created() {
    const postsData = localStorage.getItem("posts");
    if (!postsData) {
      fetch("https://jsonplaceholder.typicode.com/posts")
        .then((response) => response.json())
        .then((posts) => {
          this.posts = posts;
          localStorage.setItem("posts", JSON.stringify(posts));
        });
    } else {
      this.posts = JSON.parse(postsData);
    }
    // Сделать запрос и забрать список постов
    // Будем сравнивать ответ сервера и перезаписывать в него изменения пользователя
    // const tickersData = localStorage.getItem("edited-posts");
  },
  computed: {
    searchedPosts() {
      return this.posts.filter((post) => post.title.includes(this.search));
    },
  },
  methods: {
    showButtons() {
      console.log("123");
    },
    disableChanges(newBody) {
      if (newBody === undefined) {
        return;
      }
      const newForm = () => (this.form[Object.keys(this.form)[0]] = "");
      this.form = newForm;
    },
    saveChanges(changedPost, newBody) {
      if (newBody === undefined) {
        return;
      }
      this.posts = this.posts.map((post) => {
        if (post === changedPost) {
          const updatedPost = {
            ...post,
            body: newBody,
          };
          post = updatedPost;
        }
        return post;
      });
      localStorage.setItem("posts", JSON.stringify(this.posts));
      const newForm = () => (this.form[Object.keys(this.form)[0]] = "");
      this.form = newForm;
    },
    handleDelete(postToRemove) {
      this.posts = this.posts.filter((post) => post !== postToRemove);
      localStorage.setItem("posts", JSON.stringify(this.posts));
    },
    saveEditedPost() {
      // Нужно для сохранения в локал сторедж
      localStorage.setItem("edited-posts", JSON.stringify(this.tickers));
    },
  },
};
</script>

<style src="./app.css"></style>
<style lang="scss"></style>