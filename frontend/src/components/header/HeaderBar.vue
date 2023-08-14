<template>
  
</template>

<script>
import { logoURL } from "@/utils/constants";


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
