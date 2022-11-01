<template>
  <main>
    <header class="prose lg:prose-xl mb-7">
      <h1>Samstag</h1>
    </header>
    <editor-input class="editor prose lg:prose-xl mb-7" v-model="content" />
  </main>
</template>

<script>
import EditorInput from "./components/EditorInput.vue";

export default {
  name: "App",
  components: {
    EditorInput,
  },
  data() {
    return {
      content: {
        type: "doc",
        content: [
          {
            type: "paragraph",
            content: [
              {
                type: "text",
                text: "Insert samstag text here.",
              },
            ],
          },
        ],
      },
    };
  },
};
</script>

<style scoped></style>
