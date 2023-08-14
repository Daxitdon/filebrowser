<template>
  <div class="dashboard">
    <header-bar showMenu showLogo />

    <div id="nav">
      <div class="wrapper">
        <ul>
          
        </ul>
      </div>
    </div>

    <div v-if="loading">
      <h2 class="message delayed">
        <div class="spinner">
          <div class="bounce1"></div>
          <div class="bounce2"></div>
          <div class="bounce3"></div>
        </div>
        <span>{{ $t("files.loading") }}</span>
      </h2>
    </div>

    <router-view></router-view>
  </div>
</template>

<script>
import { mapState } from "vuex";


export default {
  name: "settings",
  components: {
    HeaderBar,
  },
  computed: {
    ...mapState(["user", "loading"]),
  },
};
</script>
