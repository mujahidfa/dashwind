<template>
  <div
    class="w-1/2 h-screen border-r md:w-1/3 lg:w-64 md:top-0 md:left-0"
    :class="backgroundColor"
  >
    <div class="flex items-center w-full h-20 px-4 mb-8 border-b">
      <p class="pl-2 text-2xl font-bold text-white">Dashwind</p>
    </div>

    <nav class="px-4 space-y-1">
      <a
        href="#"
        v-for="(item, index) in menuSubItems"
        :key="index"
        :class="[itemsColor, menuSubItem, index === 0 ? hoverColor : null]"
      >
        <component :is="`ItemIcon${index + 1}`" v-if="includeIcon" />
        <span class="menu-sub-item-text">{{ item }}</span>
      </a>
    </nav>
  </div>
</template>

<script>
import ItemIcon1 from "./svg/ItemIcon1.vue";
import ItemIcon2 from "./svg/ItemIcon2.vue";
import ItemIcon3 from "./svg/ItemIcon3.vue";
import ItemIcon4 from "./svg/ItemIcon4.vue";
import ItemIcon5 from "./svg/ItemIcon5.vue";

export default {
  name: "Sidebar",
  components: {
    ItemIcon1,
    ItemIcon2,
    ItemIcon3,
    ItemIcon4,
    ItemIcon5
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
      default: false
    }
  },
  data() {
    return {
      menuSubItems: [
        "Dashboard",
        "Analytics",
        "Inventory",
        "Products",
        "Settings"
      ],
      isFirstItem: true
    };
  },
  computed: {
    backgroundColor() {
      let color = this.themeColor;
      return `bg-${color}-500`;
    },
    itemsColor() {
      let color = this.themeColor;
      return `text-${color}-200 hover:bg-${color}-600`;
    },
    hoverColor() {
      return `bg-${this.themeColor}-600`;
    },
    menuSubItem() {
      let paddings = [2, 3, 4, 5];
      let padding = paddings[(paddings.length * Math.random()) | 0];

      return `flex items-center py-${padding} px-4 rounded-${this.borderRadius} hover:shadow-${this.borderRadius}`;
    }
  }
};
</script>

<style scoped>
.menu-sub-header {
  @apply pl-4 text-sm font-semibold mb-1 text-white;
}

.menu-sub-item {
  /* @apply flex items-center py-4 px-4 */
  /* @apply w-full flex items-center h-10 pl-4 rounded-lg; */
  @apply flex items-center py-2 px-4 rounded-lg;
}

.menu-sub-item-text {
  @apply text-white;
}
</style>
