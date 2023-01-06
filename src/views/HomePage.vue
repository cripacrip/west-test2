<template>
    <div class="home">
        <div class="input-div">
            <div class="inputs">
                <input type="text" v-model="query">
            </div>
            <div class="querys" v-html="replaceQuery">
            </div>
            <!-- <div class="replace_text">
                {{  this.text  }}
            </div> -->
        </div>
        <h1 class="title">Welcome to APP!</h1>
        <!-- <img src="@/assets/background.svg" alt="img"> -->

        <FileMultiplePreview></FileMultiplePreview>



        <transition v-if="showModal" name="modal">
        <div class="modal-mask">
          <div class="modal-wrapper">
            <div class="modal-container">

              <div class="modal-header">
                <slot name="header">
                  default header
                </slot>
              </div>

              <div class="modal-body">
                <slot name="body">
                  default body
                </slot>
              </div>

              <div class="modal-footer">
                <slot name="footer">
                  default footer
                  <button class="modal-default-button" @click="$emit('close')">
                    OK
                  </button>
                </slot>
              </div>
            </div>
          </div>
        </div>
      </transition>
    </div>
</template>

<script>
// import FilePreview from '../components/FilePreview.vue';
import FileMultiplePreview from '../components/FileMultiplePreview.vue';
// FileMultiplePreview

export default {
    data() {
        return {
            text: 'Mrs Luna, Hello',
            query: '',
            showModal: false,
        }
    },
    components: {
        // FilePreview,
        FileMultiplePreview
    },
    computed: {
        replaceQuery() {
            return this.text.replace(this.query, match => `<span style="background: yellow" >${match}</span>`)
        },
    }
}
</script>

<style lang="scss" scoped>
.input-div {
    display: flex;
    flex-direction: column;
}

.highlight {
    background-color: yellow;
    width: 100px;
}


.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: table;
  transition: opacity 0.3s ease;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}

.modal-container {
  width: 300px;
  margin: 0px auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
  font-family: Helvetica, Arial, sans-serif;
}

.modal-header h3 {
  margin-top: 0;
  color: #42b983;
}

.modal-body {
  margin: 20px 0;
}

.modal-default-button {
  float: right;
}

/*
 * The following styles are auto-applied to elements with
 * transition="modal" when their visibility is toggled
 * by Vue.js.
 *
 * You can easily play with the modal transition by editing
 * these styles.
 */

.modal-enter {
  opacity: 0;
}

.modal-leave-active {
  opacity: 0;
}

.modal-enter .modal-container,
.modal-leave-active .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}
</style>