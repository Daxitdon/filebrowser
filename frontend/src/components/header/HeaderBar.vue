<template>
  <header>
    <img v-if="showLogo !== undefined" :src="logoURL" />
    

    <slot />

    <div id="dropdown" :class="{ active: this.$store.state.show === 'more' }">
      <slot name="actions" />
    </div>

    

    <div
      class="overlay"
      v-show="this.$store.state.show == 'more'"
      @click="$store.commit('closeHovers')"
    />
  </header>
</template>

<script>
import { logoURL } from "@/utils/constants";

import Action from "@/components/header/Action";

export default {
  name: "header-bar",
  props: ["showLogo", "showMenu"],
  components: {
    Action,
  },
  data: function () {
    return {
      logoURL,
    };
  },
  methods: {
    openSidebar() {
      this.$store.commit("showHover", "sidebar");
    },
  },
};
</script>

<style></style>
