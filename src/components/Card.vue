<template>
  <div>
    <h6 class="mb-3 text-base text-gray-900 lg:text-xl dark:text-white">
      {{ post.id }}
    </h6>
    <h3
      class="
        mb-3
        text-base
        font-semibold
        text-gray-900
        lg:text-xl
        dark:text-white
      "
    >
      {{ post.title }}
    </h3>

    <p
      @click="isClicked = true"
      class="
        text-sm
        font-normal
        cursor-pointer
        text-gray-500
        dark:text-gray-400
      "
    >
      {{ post.body }}
    </p>
    <div v-if="isClicked">
      <div class="mt-1 relative rounded-md shadow-md">
        <div class="flex justify-center">
          <textarea
            ref="input"
            v-model="form[post.id]"
            class="
              form-control
              block
              w-full
              px-3
              py-1.5
              text-base
              font-normal
              text-gray-700
              bg-white bg-clip-padding
              border border-solid border-gray-300
              rounded
              transition
              ease-in-out
              m-0
              focus:text-gray-700
              focus:bg-white
              focus:border-blue-600
              focus:outline-none
            "
            id="exampleFormControlTextarea1"
            rows="3"
            placeholder="type new text ..."
          ></textarea>
        </div>
      </div>
      <ul class="my-4 space-y-3">
        <li>
          <button
            @click="save()"
            href="#"
            class="
              flex
              w-full
              items-center
              p-3
              text-base
              font-bold
              text-gray-900
              bg-gray-50
              rounded-lg
              hover:bg-gray-100
              group
              hover:shadow
              dark:bg-gray-600 dark:hover:bg-gray-500 dark:text-white
            "
          >
            <span class="flex-1 ml-3 whitespace-nowrap">Save Changes</span>
          </button>
        </li>
        <li>
          <button
            @click="$emit('disableChanges')"
            href="#"
            class="
              flex
              w-full
              items-center
              p-3
              text-base
              font-bold
              text-gray-900
              bg-gray-50
              rounded-lg
              hover:bg-gray-100
              group
              hover:shadow
              dark:bg-gray-600 dark:hover:bg-gray-500 dark:text-white
            "
          >
            <span class="flex-1 ml-3 whitespace-nowrap">Disable Changes</span>
          </button>
        </li>
        <li>
          <button
            @click="$emit('handleDelete')"
            href="#"
            class="
              flex
              items-center
              w-full
              p-3
              text-base
              font-bold
              text-gray-900
              bg-gray-50
              rounded-lg
              hover:bg-gray-100
              group
              hover:shadow
              dark:bg-gray-600 dark:hover:bg-gray-500 dark:text-white
            "
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
  props: ["post", "form", "index"],
  data() {
    return {
      isClicked: false,
    };
  },
  created() {
    this.firstThreePosts(this.index);
  },
  watch: {
    index: function (newVal) {
      this.firstThreePosts(newVal);
    },
  },
  methods: {
    save() {
      if (this.$refs.input.value) {
        this.$emit("saveChanges");

        this.isClicked = false;
      }
    },
    firstThreePosts(value) {
      if (value < 3) {
        this.isClicked = true;
      }
    },
  },
};
</script>
