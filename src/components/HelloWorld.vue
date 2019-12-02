<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div class="spacer-top">
      <button
        class="btn btn-primary"
        @click="handleOpenCompositionModal">
        composition modal
      </button>
      <button
        class="btn btn-primary spacer-left"
        @click="handleOpenOptionsModal">
        options modal
      </button>
    </div>
    <modal-composition
      :show-modal="showCompositionModal"
      @onCloseModal="handleCloseCompositionModal"
    >
      <h2 class="modal-heading">Composition API</h2>
    </modal-composition>
    <modal-options
      :show-modal="showOptionsModal"
      @onCloseModal="handleCloseOptionsModal"
    >
      <h2 class="modal-heading">Options API</h2>
    </modal-options>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import ModalComposition from '@/components/ModalComposition.vue'
import ModalOptions from '@/components/ModalOptions.vue'

export default Vue.extend({
  name: 'HelloWorld',
  components: { ModalComposition, ModalOptions },
  props: {
    msg: String,
  },
  data() {
    return {
      showCompositionModal: false,
      showOptionsModal: false
    }
  },
  methods: {
    handleOpenCompositionModal() {
      this.showCompositionModal = true
    },
    handleOpenOptionsModal() {
      this.showOptionsModal = true
    },
    handleCloseCompositionModal() {
      this.showCompositionModal = false
    },
    handleCloseOptionsModal() {
      this.showOptionsModal = false
    }
  }
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.spacer-left {
  margin-left: 8px;
}
.spacer-top {
  margin-top: 16px;
}
</style>
