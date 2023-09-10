<template>
  <div class="app-wrap">
    <div class="pages-wrp">
      <PageList :pages="pages" @add-page="addPage" @select-page="selectPage" @remove-page="removePage" />
    </div>
    <div class="editor-wrap">
      <GrapesJS />
    </div>
  </div>
</template>

<script>
import GrapesJS from "./GrapesJS.vue";
import PageList from "./PageList.vue";

export default {
  components: {
    GrapesJS,
    PageList,
  },
  data() {
    return {
      pages: [],
    };
  },
  mounted() {
    this.setPages(pm.getAll());
    editor.on("page", () => {
      this.pages = [...pm.getAll()];
    });
  },
  methods: {
    setPages(pages) {
      this.pages = [...pages];
    },
    isSelected(page) {
      return pm.getSelected().id === page.id;
    },
    selectPage(pageId) {
      return pm.select(pageId);
    },
    removePage(pageId) {
      return pm.remove(pageId);
    },
    addPage() {
      const len = pm.getAll().length;
      pm.add({
        name: `Page ${len + 1}`,
        component: '<div>New page</div>',
      });
    },
  },
};
</script>
