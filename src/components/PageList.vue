<template>
  <div class="pages">
    <div v-for="page in pages" :key="page.id" :class="{ page: 1, selected: isSelected(page) }" @click="selectPage(page.id)">
      {{ page.name || page.id }} <span v-if="!isSelected(page)" @click="removePage(page.id)" class="page-close">&Cross;</span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    pages: Array,
  },
  methods: {
    isSelected(page) {
      return pm.getSelected().id === page.id;
    },
    selectPage(pageId) {
      return pm.select(pageId);
    },
    removePage(pageId) {
      return pm.remove(pageId);
    },
  },
};
</script>
