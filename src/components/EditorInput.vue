<template>
  <editor-content class="editor" :editor="editor" />
</template>

<script>
import { Editor, EditorContent } from "@tiptap/vue-3";
import { Bold } from "@tiptap/extension-bold";
import { BulletList } from "@tiptap/extension-bullet-list";
import { Document } from "@tiptap/extension-document";
import { Dropcursor } from "@tiptap/extension-dropcursor";
import { Gapcursor } from "@tiptap/extension-gapcursor";
import { HardBreak } from "@tiptap/extension-hard-break";
import { Heading } from "@tiptap/extension-heading";
import { History } from "@tiptap/extension-history";
import { Italic } from "@tiptap/extension-italic";
import { ListItem } from "@tiptap/extension-list-item";
import { OrderedList } from "@tiptap/extension-ordered-list";
import { Paragraph } from "@tiptap/extension-paragraph";
import { Text } from "@tiptap/extension-text";

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
      extensions: [
        Bold,
        BulletList,
        Document,
        Dropcursor,
        Gapcursor,
        HardBreak,
        Heading.configure({ levels: [2] }),
        History,
        Italic,
        ListItem,
        OrderedList,
        Paragraph,
        Text,
      ],
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
