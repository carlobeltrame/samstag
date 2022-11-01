<template>
  <editor-content class="editor" :editor="editor" />
</template>

<script>
import { Editor, EditorContent } from "@tiptap/vue-3";
import StarterKit from "@tiptap/starter-kit";

export default {
  name: "EditorInput",
  components: {
    EditorContent,
  },
  props: {
    modelValue: {
      type: Object,
      default: () => ({ type: "doc", content: [{ type: "paragraph" }] }),
    },
  },
  emits: ["update:modelValue"],
  data() {
    return {
      editor: null,
    };
  },
  watch: {
    modelValue(value) {
      const isSame =
        JSON.stringify(this.editor.getJSON()) === JSON.stringify(value);
      if (isSame) {
        return;
      }

      this.editor.commands.setContent(value, false);
    },
  },
  mounted() {
    this.editor = new Editor({
      extensions: [StarterKit],
      content: this.modelValue,
      onUpdate: () => {
        this.$emit("update:modelValue", this.editor.getJSON());

      },
    });
  },
  beforeUnmount() {
    this.editor.destroy();
  },
};
</script>

<style scoped></style>
