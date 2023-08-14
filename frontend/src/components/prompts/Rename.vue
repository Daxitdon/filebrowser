<template>
  <div class="card floating">
    <div class="card-title">
      <h2>{{ $t("prompts.rename") }}</h2>
    </div>

    <div class="card-content">
      <p>
        {{ $t("prompts.renameMessage") }} <code>{{ oldName() }}</code
        >:
      </p>
      <input
        class="input input--block"
        v-focus
        type="text"
        @keyup.enter="submit"
        v-model.trim="name"
      />
    </div>

    
  </div>
</template>

<script>
import { mapState, mapGetters } from "vuex";
import url from "@/utils/url";
import { files as api } from "@/api";

export default {
  name: "rename",
  data: function () {
    return {
      name: "",
    };
  },
  created() {
    this.name = this.oldName();
  },
  computed: {
    ...mapState(["req", "selected", "selectedCount"]),
    ...mapGetters(["isListing"]),
  },
  methods: {
    cancel: function () {
      this.$store.commit("closeHovers");
    },
    oldName: function () {
      if (!this.isListing) {
        return this.req.name;
      }

      if (this.selectedCount === 0 || this.selectedCount > 1) {
        // This shouldn't happen.
        return;
      }

      return this.req.items[this.selected[0]].name;
    },
    submit: async function () {
      let oldLink = "";
      let newLink = "";

      if (!this.isListing) {
        oldLink = this.req.url;
      } else {
        oldLink = this.req.items[this.selected[0]].url;
      }

      newLink =
        url.removeLastDir(oldLink) + "/" + encodeURIComponent(this.name);

      try {
        await api.move([{ from: oldLink, to: newLink }]);
        if (!this.isListing) {
          this.$router.push({ path: newLink });
          return;
        }

        this.$store.commit("setReload", true);
      } catch (e) {
        this.$showError(e);
      }

      this.$store.commit("closeHovers");
    },
  },
};
</script>
