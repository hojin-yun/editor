<template>
  <div class="hello">
    <quill-editor
      ref="myQuillEditor"
      v-model="content"
      :options="editorOption"
      @blur="onEditorBlur($event)"
      @focus="onEditorFocus($event)"
      @ready="onEditorReady($event)"
      style="height: 500px"
    />
    <div>
      <h2>I am Example</h2>
      <p><br /></p>
      <p>acaca</p>
      <p>cascsac</p>
      <p>
        <img
          src="data:image/gif;base64,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"
        />
      </p>
      <p>sdvvsdvsdv</p>
    </div>

    <button @click="editorHhtml">aaa</button>
    <!-- <quill-editor
      :content="content"
      :options="editorOption"
      @change="onEditorChange($event)"
    /> -->
  </div>
</template>

<script>
import "quill/dist/quill.core.css";
import "quill/dist/quill.snow.css";
import "quill/dist/quill.bubble.css";

import { quillEditor } from "vue-quill-editor";
export default {
  components: {
    quillEditor,
  },
  data() {
    return {
      content: "<h2>I am Example</h2>",
      editorOption: {
        // Some Quill options...
        modules: {
          toolbar: [
            ["bold", "italic", "underline", "strike"],
            //["blockquote", "code-block"],
            [{ header: 1 }, { header: 2 }],
            [{ list: "ordered" }, { list: "bullet" }],
            [{ script: "sub" }, { script: "super" }],
            [{ indent: "-1" }, { indent: "+1" }],
            [{ direction: "rtl" }],
            [{ size: ["small", false, "large", "huge"] }],
            [{ header: [1, 2, 3, 4, 5, 6, false] }],
            //[{ font: [] }],
            [{ color: [] }, { background: [] }],
            [{ align: [] }],
            ["clean"],
            ["link", "image", "video"],
          ],
          // toolbar: {
          //   container: [
          //     // Toolbar configuration, default is all
          //     ["bold"],
          //     ["italic"],
          //     ["underline"],
          //     ["strike"],
          //     [{ size: ["small", false, "large", "huge"] }],
          //     [{ list: "ordered" }, { list: "bullet" }],
          //     ["link"],
          //     ["image"],
          //     ["table"],
          //   ],
          //   handlers: {
          //     // image: function (value) {
          //     //   console.log(value);
          //     // },
          //   },
          // },
        },
      },
    };
  },
  methods: {
    onEditorBlur() {
      //console.log("editor blur!", quill);
    },
    onEditorFocus() {
      //console.log("editor focus!", quill);
    },
    onEditorReady(editor) {
      // editor
      //   .getModule("toolbar")
      //   .addHandler("image", () => this.imageHandler(editor));
      console.log("editor ready!", editor.getSelection());
    },
    imageHandler: async function (editor) {
      const input = document.createElement("input");

      input.setAttribute("type", "file");
      input.setAttribute("accept", "image/*");
      input.click();
      console.log(input);

      input.onchange = async () => {
        const file = input.files[0];
        const formData = new FormData();
        console.log(input);
        console.log(file.name);
        console.log(formData);

        formData.append("file", file);

        // Save current cursor state
        const range = editor.getSelection(true);
        console.log(range.index);
        console.log(formData);
        // await axios
        //   .post("/admin/media", formData)
        //   .then(async ({ data }) => {
        //     // Insert uploaded image
        //     await editor.insertEmbed(range.index, "image", data.link);
        //   })
        //   .catch(({ response }) => {
        //     alert("error");
        //   });
      };
    },
    onEditorChange({ quill, html, text }) {
      console.log("editor change!", quill, html, text);
      this.content = html;
    },
    editorHhtml() {
      console.log(this.content);
    },
  },
  computed: {
    editor() {
      return this.$refs.myQuillEditor.quill;
    },
  },
  mounted() {
    //console.log("this is current quill instance object", this.editor);
  },
};
</script>
