<template>
  <section class="bg-white dark:bg-gray-900">
    <div class="py-8 px-4 mx-auto max-w-2xl lg:py-16">
      <h2 class="mb-4 text-xl font-bold text-gray-900 dark:text-white">
        Add a new category
      </h2>
      <form action="#" @submit="addNewCategory">
        <div class="grid gap-4 sm:grid-cols-2 sm:gap-6">
          <div class="sm:col-span-2">
            <label
              for="name"
              class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
              >Enter ftitle category</label
            >
            <input
              v-model="title"
              type="text"
              name="name"
              id="name"
              class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-primary-500 dark:focus:border-primary-500"
              placeholder="Enter title"
              required=""
            />
          </div>
        </div>

        <button
          type="submit"
          class="inline-flex items-center px-5 py-2.5 mt-4 sm:mt-6 text-sm font-medium text-center text-white bg-primary-700 rounded-lg focus:ring-4 focus:ring-primary-200 dark:focus:ring-primary-900 hover:bg-primary-800"
        >
          Add New Category
        </button>
      </form>
    </div>
  </section>
</template>
<script>
import { toast } from "vue3-toastify";

export default {
  name: "AdminAdd",
  data() {
    return {
      title: "",
    };
  },

  methods: {
    addNewCategory(e) {
      e.preventDefault();

      const newcategory = {
        title: this.title,
      };

      if (!newcategory.title.trim()) {
        toast.warning("Please enter title");
      } else {
        this.$store.dispatch("ADD_CATEGORY", newcategory).then((res) => {
          if (res) {
            toast.success("added successfully new category");
            window.location.replace("/category/list");
          } else {
            toast.error(this.$store.state.category.authMessage);
          }
        });
      }
    },
  },
};
</script>
<style lang="css"></style>
