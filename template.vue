<script lang="ts" setup>
import { useLocalStorage } from "@vueuse/core";
import 'hf-richtext/dist/style.css'
import {
  ExtensionAudio,
  ExtensionBlockquote,
  ExtensionBold,
  ExtensionBulletList,
  ExtensionClearFormat,
  ExtensionCode,
  ExtensionCodeBlock,
  ExtensionColor,
  ExtensionColumn,
  ExtensionColumns,
  ExtensionCommands,
  ExtensionDocument,
  ExtensionDraggable,
  ExtensionDropcursor,
  ExtensionFontSize,
  ExtensionFormatBrush,
  ExtensionGapcursor,
  ExtensionHardBreak,
  ExtensionHeading,
  ExtensionHighlight,
  ExtensionHistory,
  ExtensionHorizontalRule,
  ExtensionIframe,
  ExtensionImage,
  ExtensionIndent,
  ExtensionItalic,
  ExtensionLink,
  ExtensionListKeymap,
  ExtensionNodeSelected,
  ExtensionOrderedList,
  ExtensionPlaceholder,
  ExtensionRangeSelection,
  ExtensionSearchAndReplace,
  ExtensionStrike,
  ExtensionSubscript,
  ExtensionSuperscript,
  ExtensionTable,
  ExtensionTaskList,
  ExtensionText,
  ExtensionTextAlign,
  ExtensionTrailingNode,
  ExtensionUnderline,
  ExtensionVideo,
  RichTextEditor,
  lowlight,
  useEditor,
  ExtensionTextDiagram,
} from "hf-richtext";

const content = useLocalStorage("content", "");

const editor = useEditor({
  content: content.value,
  extensions: [
    ExtensionBlockquote,
    ExtensionBold,
    ExtensionBulletList,
    ExtensionCode,
    ExtensionDocument,
    ExtensionDropcursor.configure({
      width: 2,
      class: "dropcursor",
      color: "skyblue",
    }),
    ExtensionGapcursor,
    ExtensionHardBreak,
    ExtensionHeading,
    ExtensionHistory,
    ExtensionHorizontalRule,
    ExtensionItalic,
    ExtensionOrderedList,
    ExtensionStrike,
    ExtensionText,
    ExtensionImage.configure({
      HTMLAttributes: {
        loading: "lazy",
      },
    }),
    ExtensionTaskList,
    ExtensionLink.configure({
      autolink: false,
      openOnClick: false,
    }),
    ExtensionTextAlign.configure({
      types: ["heading", "paragraph"],
    }),
    ExtensionUnderline,
    ExtensionTable.configure({
      resizable: true,
    }),
    ExtensionSubscript,
    ExtensionSuperscript,
    ExtensionPlaceholder.configure({
      placeholder: "输入 / 以选择输入类型",
    }),
    ExtensionHighlight,
    ExtensionVideo,
    ExtensionAudio,
    ExtensionCommands,
    ExtensionCodeBlock.configure({
      lowlight,
    }),
    ExtensionIframe,
    ExtensionColor,
    ExtensionFontSize,
    ExtensionIndent,
    ExtensionDraggable,
    ExtensionColumns,
    ExtensionColumn,
    ExtensionNodeSelected,
    ExtensionTrailingNode,
    ExtensionListKeymap,
    ExtensionSearchAndReplace,
    ExtensionClearFormat,
    ExtensionFormatBrush,
    ExtensionRangeSelection,
    ExtensionTextDiagram,
  ],
  parseOptions: {
    preserveWhitespace: true,
  },
  onUpdate: () => {
    content.value = editor.value?.getHTML() + "";
  },
});
</script>

<template>
  <div style="height: 100vh" class="flex">
    <RichTextEditor v-if="editor" :editor="editor" />
  </div>
</template>
