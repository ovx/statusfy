<template>
  <div class="header">
    <component :is="titleTag" class="title">
      {{ $t("title") }}
    </component>

    <client-only>
      <Subscribe v-if="displaySubscribe" class="subscribe-container" />
    </client-only>
  </div>
</template>

<script>
import Subscribe from "./Subscribe";

export default {
  components: {
    Subscribe
  },
  props: {
    titleTag: {
      type: String,
      default: "div"
    }
  },
  computed: {
    displaySubscribe() {
      if (
        this.$statusfy.notifications &&
        typeof this.$statusfy.notifications === "object"
      ) {
        return !!Object.values(this.$statusfy.notifications).find(v => v);
      } else {
        return false;
      }
    }
  }
};
</script>

<style scoped>
.title {
  color: var(--grey-darkest);
}
</style>
