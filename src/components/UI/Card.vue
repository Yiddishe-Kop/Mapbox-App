<template>
  <div class="card">
    <div v-if="title" class="header">{{title}}</div>
    <div class="body">
      <slot />
    </div>
    <div v-if="footer" class="footer">{{footer}}</div>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: ["title", "footer"]
};
</script>

<style lang="scss">
.card {
  @apply py-2;
  .header {
    @apply text-lg font-bold pb-2 mb-2;
  }
  .body {
    @apply bg-gray-700 px-4 py-2;
  }
}
</style>
