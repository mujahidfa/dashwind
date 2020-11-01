<template>
  <div class="flex flex-col max-w-screen-lg mx-auto">
    <!-- Header -->
    <header
      role="banner"
      class="flex flex-col items-center justify-center px-4 pt-20 pb-4 text-center"
    >
      <h1
        class="text-6xl font-semibold text-transparent bg-clip-text bg-gradient-to-r from-pink-400 to-indigo-400"
      >
        Dashwind
      </h1>
      <p class="text-2xl tracking-wide text-pink-100">
        Generate dashboard navbar templates at a click of a button.
      </p>
      <p class="text-2xl tracking-wide text-indigo-100">
        Use
        <a
          href="https://tailwindcss.com/"
          target="_blank"
          rel="noopener noreferrer"
          class="text-teal-200 transition duration-700 ease-in-out transform hover:tracking-widest hover:font-bold hover:text-teal-300 hover:scale-150"
          >TailwindCSS</a
        >
        and hit those deadlines.
      </p>
    </header>

    <!-- Dashboard view -->
    <div
      class="flex justify-center p-2 m-8 bg-gray-100 border border-gray-500 rounded-xl"
    >
      <div class="w-full h-3/4" id="dashboard">
        <Dashboard
          :themeColor="themeColor"
          :borderRadius="borderRadius"
          :includeIcon="includeIcon"
        />
      </div>
    </div>

    <!-- Options -->
    <div
      class="flex flex-col items-center justify-center space-y-2 sm:space-y-0 sm:space-x-4 sm:flex-row"
    >
      <button :class="[optionsButtonStyle]" @click="randomizeThemes()">
        Change theme
      </button>
      <button :class="[optionsButtonStyle]" @click="toggleIcon()">
        Toggle Icon
      </button>
      <!-- <button :class="[optionsButtonStyle]" @click="toggleBackgroundTheme()">
        Toggle light/dark background
      </button> -->
      <button :class="[optionsButtonStyle]" @click="copyTemplate()">
        Copy code
      </button>
    </div>

    <!-- Code block -->
    <div
      class="flex justify-center p-6 text-sm overscroll-auto"
      style="height: 28rem;"
      ref="codeBlock"
    >
      <pre
        class="border-4 border-gray-300 rounded-xl language-html"
      ><code>{{ dashboardTemplate }}</code></pre>
    </div>

    <!-- Footer -->
    <footer
      class="flex items-center justify-center py-4 pb-12 space-x-2 text-center text-white"
    >
      <p>
        Made by
        <a
          href="https://twitter.com/mujahid_fa"
          target="_blank"
          rel="noopener noreferrer"
          :class="
            `text-${themeColor}-300 transition duration-700 ease-in-out transform hover:tracking-widest hover:font-semibold hover:text-${themeColor}-500 hover:scale-150`
          "
          >Mujahid Anuar</a
        >
        ✌️
      </p>
      <!-- <p class="flex items-center justify-center">.</p> -->
      <p>
        on
        <a
          href="https://github.com/mujahidfa/dashwind"
          target="_blank"
          rel="noopener noreferrer"
          class="text-blue-200 transition duration-700 ease-in-out transform hover:tracking-widest hover:font-semibold hover:text-blue-300 hover:scale-150"
          >GitHub</a
        >
      </p>
    </footer>
  </div>
</template>

<script>
// import Sidebar from "./components/Sidebar.vue";
// import Navbar from "./components/Navbar.vue";
import Dashboard from "./components/Dashboard.vue";

import Prism from "prism-es6";
import prettier from "prettier/standalone";
import parserHtml from "prettier/parser-html";

export default {
  name: "App",
  components: {
    // Sidebar,
    Dashboard
  },
  data() {
    return {
      themeColor: "indigo",
      borderRadius: "lg",
      sidebarTemplate: "",
      dashboardTemplate: "",
      includeIcon: true
    };
  },
  computed: {
    optionsButtonStyle() {
      return `px-4 py-4 bg-${this.themeColor}-700 rounded-${this.borderRadius} hover:bg-${this.themeColor}-800 text-white`;
    }
  },
  methods: {
    randomizeThemes() {
      this.setThemeColor();
      this.setBorderRadius();
      this.formatCode();
    },
    setThemeColor() {
      const colors = [
        "red",
        "orange",
        "yellow",
        "green",
        "teal",
        "blue",
        "indigo",
        "purple",
        "pink",
        "gray"
      ];
      this.themeColor = this.randomizeArray(colors);
    },
    setBorderRadius() {
      const radius = ["none", "sm", "md", "lg", "xl", "2xl"];
      this.borderRadius = this.randomizeArray(radius);
    },
    randomizeArray(array) {
      return array[(array.length * Math.random()) | 0];
    },
    toggleIcon() {
      this.includeIcon = !this.includeIcon;
      this.formatCode();
    },
    formatCode() {
      let dashboardTemplate = document.getElementById("dashboard").innerHTML;
      dashboardTemplate = dashboardTemplate
        .replaceAll(/data-v-[\w\d]*=""/g, "")
        .replaceAll(/<!--v-if-->/g, "");
      this.dashboardTemplate = prettier.format(dashboardTemplate, {
        parser: "html",
        plugins: [parserHtml]
      });
    },
    copyTemplate() {
      navigator.clipboard
        .writeText(this.dashboardTemplate)
        .then(() => {
          alert("Template is copied!");
        })
        .catch(() => {
          alert("Sorry, unable to copy to clipboard.");
        });
    }
  },
  mounted() {
    this.formatCode();
    Prism.highlightAllUnder(this.$refs.codeBlock);
  },
  updated() {
    this.formatCode();
    Prism.highlightAllUnder(this.$refs.codeBlock);
  }
};
</script>

<style scoped>
@import "./assets/themes/prism-okaidia.css";
</style>
