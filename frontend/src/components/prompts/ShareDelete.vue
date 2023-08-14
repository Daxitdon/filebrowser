<template>
  <div class="card floating">
    <div class="card-content">
      <p>{{ $t("prompts.deleteMessageShare", { path: "" }) }}</p>
    </div>
    
  </div>
</template>

<script>
import { mapState } from "vuex";

export default {
  name: "share-delete",
  computed: {
    ...mapState(["showConfirm"]),
  },
  methods: {
    submit: function () {
      this.showConfirm();
    },
  },
};
</script>
