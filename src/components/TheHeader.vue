<template>
  <header class="px-4 py-2 border-b-2 border-white" :class="[backgroundColor]">
    <nav class="flex w-full">
      <div class="w-2/3">
        <a href="#" class="text-xl font-bold tracking-wide" :class="[textColor]"
          >Dashwind</a
        >
      </div>

      <div class="flex justify-end w-1/3">
        <div class="flex space-x-4">
          <a href="#" class="text-lg font-semibold" :class="[textColor, hover]"
            >Profile</a
          >
          <a href="#" class="text-lg font-semibold" :class="[textColor, hover]"
            >Logout</a
          >
        </div>
      </div>
    </nav>
  </header>
</template>

<script>
export default {
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
    }
  },
  computed: {
    backgroundColor() {
      return `bg-${this.themeColor}-700`;
    },
    textColor() {
      return `text-white`; //`text-${this.themeColor}-600`;
    },
    hover() {
      return `hover:bg-${this.themeColor}-900 px-3 py-1 rounded-${this.borderRadius} hover:shadow-${this.borderRadius}`;
    }
  }
};
</script>

<style scoped></style>
