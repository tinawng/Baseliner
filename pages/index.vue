<template>
  <div class="page__container" :style="css_style">
    <div class="page__header">
      <h2>Baseline Generator</h2>
    </div>
    <div class="sentence__container">
      <h1>{{sentence}}</h1>
    </div>
    <div class="page__footer">
      <svg ref="refresh-button" class="refresh_button" @click="refresh" viewBox="0 0 520 520">
        <path fill="none" d="M0 0h520v520H0z"></path>
        <path
          d="M260 60V0l100 100-100 100v-60c-66.274 0-120 53.726-120 120H60c0-110.457 89.543-200 200-200zm0 400v60L160 420l100-100v60c66.274 0 120-53.726 120-120h80c0 110.457-89.543 200-200 200z"
          fill="currentColor"
        ></path>
      </svg>
    </div>
  </div>
</template>

<script>
import colors from "~/assets/json/colors.json";
import adjectives from "~/assets/json/adjectives.json";
import garnishes from "~/assets/json/garnishes.json";
import nouns from "~/assets/json/nouns.json";
export default {
  data: () => ({
    refresher: 0,
  }),
  computed: {
    css_style: function () {
      let dummy = this.refresher;
      let color = colors[Math.floor(Math.random() * colors.length)];
      let r = Math.random();
      return `--text-color: ${r > 0.5 ? color.light : color.dark}; --bg-color: ${r > 0.5 ? color.dark : color.light};`;
    },
    sentence: function () {
      let dummy = this.refresher;
      let adjective = adjectives[Math.floor(Math.random() * adjectives.length)];
      let garnish = garnishes[Math.floor(Math.random() * garnishes.length)];
      while (garnish === adjective) {
        garnish = garnishes[Math.floor(Math.random() * garnishes.length)];
      }

      let noun = nouns[Math.floor(Math.random() * nouns.length)];
      return `${adjective} ${garnish} ${noun}`;
    },
  },

  methods: {
    refresh() {
      this.refresher = Math.random();
      this.$refs["refresh-button"].classList.add("spint_it");
      setTimeout(() => {
        this.$refs["refresh-button"].classList.remove("spint_it");
      }, 500);
    },
  },
};
</script>

<style lang="postcss">
.page__container {
  @apply h-screen w-screen;
  padding: 1vw;
  @apply flex flex-col;
  @apply overflow-hidden;

  color: var(--text-color);
  background-color: var(--bg-color);
}
.page__header {
  @apply pt-1;
  border-color: var(--text-color);
  @apply border-t-2;
}

.sentence__container {
  @apply flex-grow;
  @apply flex justify-start items-center;
  @apply capitalize;
}

.page__footer {
  @apply flex justify-end;
}
.refresh_button {
  @apply w-20;
  @apply cursor-pointer;
}
.spint_it {
  animation: spin .5s ease-in-out 1;
}
</style>
