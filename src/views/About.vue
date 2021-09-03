<template>
  <div>
    <div id="editor" ref="toastuiEditor"></div>

    <button @click="aaaaa">aaa</button>
  </div>
</template>

<script>
import "tui-color-picker/dist/tui-color-picker.css";
import "@toast-ui/editor-plugin-color-syntax/dist/toastui-editor-plugin-color-syntax.css";
import "@toast-ui/editor-plugin-table-merged-cell/dist/toastui-editor-plugin-table-merged-cell.css";
import "@toast-ui/editor/dist/toastui-editor.css";
import { Editor } from "@toast-ui/editor";
import colorSyntax from "@toast-ui/editor-plugin-color-syntax";
import tableMergedCell from "@toast-ui/editor-plugin-table-merged-cell";
var editor;
export default {
  data() {
    return {
      content: "",
      editorHtml: "",
    };
  },
  mounted() {
    editor = new Editor({
      el: document.querySelector("#editor"),
      previewStyle: "vertical",
      //   height: "400px",
      //   initialEditType: "markdown",
      useCommandShortcut: false,
      useDefaultHTMLSanitizer: false,
      usageStatistics: false,
      hideModeSwitch: true,
      initialEditType: "wysiwyg",
      toolbarItems: [
        ["heading", "bold", "italic", "strike"],
        ["hr"],
        ["ul", "ol", "indent", "outdent"],
        ["table", "image", "link"],
        // ["code", "codeblock"],
        ["scrollSync"],
      ],
      initialValue: this.content,
      events: {
        change: function () {
          // console.log(editor.getMarkdown());
          // console.log(editor.getHtml());
        },
      },
      plugins: [colorSyntax, tableMergedCell],
    });
    window.editor = editor;
  },
  methods: {
    aaaaa() {
      //alert(1);
      //   const aaac = document.querySelector("#editor");
      //   var content = aaac.toastuiEditor.invoke("getMarkdown");
      //console.log(this.$refs.toastuiEditor.invoke("getHTML"));
      //const mdSelection = this.editorHtml.getRangeInfoOfNode();
      //console.log(document.querySelector("#editor").textContent);
      console.dir(editor);
    },
  },
};
</script>

<style></style>
