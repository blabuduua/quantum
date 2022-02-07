<template>
  <div class="container mx-auto flex flex-col items-center bg-gray-100 p-4">
    <div class="container">
      <section>
        <div class="flex">
          <div class="max-w-xs">
            <label for="wallet" class="block text-sm font-medium text-gray-700"
              >Поиск</label
            >
            <div class="mt-1 relative rounded-md shadow-md">
              <input
                class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                id="search"
                type="text"
                placeholder="Например ipsum ..."
              />
            </div>
          </div>
        </div>
      </section>

      <hr class="w-full border-t border-gray-600 my-4" />
      <dl class="mt-5 grid grid-cols-1 gap-5 sm:grid-cols-3">
        <div class="max-w-sm rounded overflow-hidden shadow-lg bg-white">
          <div class="px-6 py-4">
            <div class="text-xl mb-2">ID</div>
            <div class="font-bold text-xl mb-2">Title</div>
            <p class="text-gray-700 text-base">Body</p>
          </div>
        </div>
      </dl>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
};
</script>

<style src="./app.css"></style>
<style lang="scss"></style>
