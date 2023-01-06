<template>
  <div class="container">
    <div class="large-12 medium-12 small-12 cell">
      <label>Files
        <input type="file" id="files" ref="files" multiple @change="handleFilesUpload()"/>
      </label>
    </div>
    <div class="large-12 medium-12 small-12 cell">
      <div class="grid-x">
        <div v-for="(file, key) in files" :key="file.name" class="files">
            <div class="files-item">
                <div class="images">
                    <img class="preview" v-bind:ref="'image'+parseInt( key )"/>
                </div>
                <div class="file_na">
                    {{ file.name }}
                </div>
            </div>
        </div>
      </div>
    </div>
    <br>
    <div class="large-12 medium-12 small-12 cell clear">
      <button v-on:click="addFiles()">Add Files</button>
    </div>
    <br>
    <div class="large-12 medium-12 small-12 cell">
      <button v-on:click="submitFiles()">Submit</button>
    </div>
  </div>
</template>

<script>
  export default {
    data(){
      return {
        files: []
      }
    },
    methods: {
      addFiles(){
        this.$refs.files.click();
      },
    //   submitFiles() {
    //     let formData = new FormData();
    //     for( var i = 0; i < this.files.length; i++ ){
    //       let file = this.files[i];
    //       formData.append('files[' + i + ']', file);
    //     }
    //     axios.post( '/file-multiple-preview',
    //       formData,
    //       {
    //         headers: {
    //             'Content-Type': 'multipart/form-data'
    //         }
    //       }
    //     ).then(function(){
    //       console.log('SUCCESS!!');
    //     })
    //     .catch(function(){
    //       console.log('FAILURE!!');
    //     });
    //   },
      handleFilesUpload(){
        let uploadedFiles = this.$refs.files.files;
        for( var i = 0; i < uploadedFiles.length; i++ ){
          this.files.push(uploadedFiles[i]);
        }
        this.getImagePreviews();
        console.log(this.files)
      },
      getImagePreviews(){
        for(let i = 0; i < this.files.length; i++){
          if (/\.(jpe?g|png|gif)$/i.test(this.files[i].name)) {
            let reader = new FileReader();
            reader.addEventListener("load", function(){
              this.$refs['image'+parseInt(i)][0].src = reader.result;
            }.bind(this), false);
            reader.readAsDataURL(this.files[i]);
          }
        }
      }
    }
  }
</script>

<style>
  input[type="file"]{
    position: absolute;
    top: -500px;
  }
  div.file-listing img{
    max-width: 90%;
  }

  .files {
    display: flex;
    justify-content: center;
  }

  .files-item {
    display: flex;
    align-items: center;
  }

  .preview {
    max-width: 100px;
    max-height: 100px;
  }
</style>