<template>
  <div>
    <h6 class="mb-3 text-base text-gray-900 lg:text-xl dark:text-white">
      {{ post.id }}
    </h6>
    <h3
      class="mb-3 text-base font-semibold text-gray-900 lg:text-xl dark:text-white"
    >
      {{ post.title }}
    </h3>

    <p
      @click="isClicked = true"
      class="text-sm font-normal cursor-pointer text-gray-500 dark:text-gray-400"
    >
      {{ post.body }}
    </p>
    <div v-if="isClicked">
      <div class="mt-1 relative rounded-md shadow-md">
        <input
          ref="input"
          v-model="form[post.id]"
          class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
          id="search"
          type="text"
          placeholder="Введите новый Body"
        />
      </div>
      <ul class="my-4 space-y-3">
        <li>
          <button
            @click="save()"
            href="#"
            class="flex w-full items-center p-3 text-base font-bold text-gray-900 bg-gray-50 rounded-lg hover:bg-gray-100 group hover:shadow dark:bg-gray-600 dark:hover:bg-gray-500 dark:text-white"
          >
            <span class="flex-1 ml-3 whitespace-nowrap">Save Changes</span>
          </button>
        </li>
        <li>
          <button
            @click="$emit('disableChanges')"
            href="#"
            class="flex w-full items-center p-3 text-base font-bold text-gray-900 bg-gray-50 rounded-lg hover:bg-gray-100 group hover:shadow dark:bg-gray-600 dark:hover:bg-gray-500 dark:text-white"
          >
            <span class="flex-1 ml-3 whitespace-nowrap">Disable Changes</span>
          </button>
        </li>
        <li>
          <button
            @click="$emit('handleDelete')"
            href="#"
            class="flex items-center w-full p-3 text-base font-bold text-gray-900 bg-gray-50 rounded-lg hover:bg-gray-100 group hover:shadow dark:bg-gray-600 dark:hover:bg-gray-500 dark:text-white"
          >
            <span class="flex-1 ml-3 whitespace-nowrap">Delete Post</span>
          </button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  props: ["post", "form"],
  data() {
    return {
      isClicked: false,
    };
  },
  methods: {
    save() {
      if (this.$refs.input.value) {
        this.$emit("saveChanges");

        this.isClicked = false;
      }
    },
  },
};
</script>
