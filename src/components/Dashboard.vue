<template>
  <TheHeader :themeColor="themeColor" :borderRadius="borderRadius" />
  <div class="flex">
    <TheSidebar
      :themeColor="themeColor"
      :borderRadius="borderRadius"
      :includeIcon="includeIcon"
    />
    <main class="flex items-center justify-center w-full">
      <!-- Insert page content here, you can remove this h1 element -->
      <h1 class="text-3xl text-gray-500 ">
        Insert content here
      </h1>
    </main>
  </div>
</template>

<script>
import TheHeader from "./TheHeader.vue";
import TheSidebar from "./TheSidebar.vue";
export default {
  components: {
    TheHeader,
    TheSidebar
  },
  props: {
    themeColor: {
      type: String,
      required: false,
      default: "blue"
    },
    borderRadius: {
      type: String,
      required: false,
      default: "3xl"
    },
    includeIcon: {
      type: Boolean,
      required: false,
      default: true
    }
  }
};
</script>

<style scoped></style>
