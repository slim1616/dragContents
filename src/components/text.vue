<template>
  <div>

     <div>{{ content }}</div>
    <vue-editor  :editorOptions="editorSettings" v-model="content" />
  </div>
</template>
<script>
import { VueEditor, Quill } from "vue2-editor";
import { ImageDrop } from "quill-image-drop-module";
import ImageResize from "quill-image-resize-module";

Quill.register("modules/imageDrop", ImageDrop);
Quill.register("modules/imageResize", ImageResize);
import axios from "axios";

export default {
    components: {
      VueEditor
    },
    data: () => ({
        content : '',
        editorSettings: {
        modules: {
            imageDrop: true,
            imageResize: {}
          }
        }
  }),
   methods: {
      handleImageAdded: function(file, Editor, cursorLocation, resetUploader) {
      // An example of using FormData
      // NOTE: Your key could be different such as:
      // formData.append('file', file)

      var formData = new FormData();
      formData.append("image", file);

      axios({
        url: "https://fakeapi.yoursite.com/images",
        method: "POST",
        data: formData
      })
        .then(result => {
          let url = result.data.url; // Get url from response
          Editor.insertEmbed(cursorLocation, "image", url);
          resetUploader();
        })
        .catch(err => {
          console.log(err);
        });
    }
    },
    computed: {
 
    },
    mounted() {
     
    }
};
</script>
