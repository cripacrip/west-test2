<template>
    <div class="container">
      <div class="large-12 medium-12 small-12 cell">
        <label>File Preview
          <input type="file" id="file" ref="file" multiple accept="image/*" @change="handleFileUpload()"/>
        </label>
        <img :src="imagePreview" class="img-preview" v-show="showPreview"/>
        <button @click="submitFile()">Submit</button>
      </div>
      <div v-for="file in files" :key="file.id">
        {{  file  }}
    </div>
    </div>
  </template>

<script>
export default {
    data() {
        return {
            file: '',
            showPreview: false,
            imagePreview: '',
            files:[],
        }
    },
    methods: {
        handleFileUpload(){
            this.file = this.$refs.file.files[0];
            let reader  = new FileReader();
            reader.addEventListener("load", function () {
                this.showPreview = true;
                this.imagePreview = reader.result;
            }.bind(this), false);
            if( this.file ){
                if ( /\.(jpe?g|png|gif)$/i.test( this.file.name ) ) {
                    reader.readAsDataURL( this.file );
                }
            }
            this.files.push(reader.readAsDataURL( this.file ))
        }
    },
}
</script>

<style scoped>
 .img-preview {
    width: 100px;
    height: 100px;
 }
</style>