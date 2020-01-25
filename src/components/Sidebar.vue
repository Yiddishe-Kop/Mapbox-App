<template>
  <div class="sidebar">
    <div v-for="(item, i) in menuItems" :key="item" class="item">
      <Icon @click.native="handleClick(i)" :icon="item" />
    </div>
  </div>
</template>

<script>
import Icon from "@/components/UI/Icon";
import markers from "@/utils/markers";

export default {
  components: { Icon },
  data() {
    return {
      menuItems: ["torah", "library", "send", "search"]
    };
  },
  methods: {
    handleClick(i) {
      this.$store.map.flyTo({
        center: markers[i].coordinates,
        speed: 1
      });
    }
  }
};
</script>

<style lang="scss">
.sidebar {
  @apply bg-gray-900 py-6;
  width: 70px;
  .item {
    cursor: pointer;
    transition: all 0.25s ease;
    @apply text-gray-50 p-4;
    &:hover {
      @apply bg-gray-800;
    }
    svg {
      height: 30px;
    }
  }
}
</style>
