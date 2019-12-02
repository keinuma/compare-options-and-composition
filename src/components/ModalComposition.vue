<template>
  <div>
    <div :class="{ 'modal-overlay': showModal }">
      <div
        v-if="showModal"
        class="modal-isshow modal-open"
      >
        <div class="modal-container">
          <button class="close-btn btn btn-outline-info" @click="closeModal">閉じる</button>
          <slot></slot>
          <div>
            <div v-show="isLastDate" class="alert alert-danger" role="alert">
              <p class="alert-last-date">
                クリスマスになりました。<br />
                アドベントカレンダーの最終日です。
              </p>
            </div>
            <p>この記事はギルドワークスアドベントカレンダーの{{ date }}日目の記事です。</p>
            <button type="button" class="btn btn-info" @click="countUpDate" :disabled="isLastDate">次の日</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import {
  createComponent,
  ref,
  computed
} from '@vue/composition-api'

type Props = {
  showModal: boolean
}

export default createComponent({
  props: {
    showModal: {
      type: Boolean,
      required: true,
      default: false
    }
  },
  setup(props: Props, context) {
    const date = ref(1)
    const isLastDate = computed(() => {
      return date.value === 25
    })
    const countUpDate = () => {
      if (isLastDate.value) {
        return
      }
      date.value++
    }
    const closeModal = (e: Event) => {
      e.stopPropagation()
      date.value = 1
      context.emit("onCloseModal")
    }
    return {
      showModal: props.showModal,
      date,
      isLastDate,
      countUpDate,
      closeModal
    }
  }
})
</script>

<style lang="scss" scoped>
.modal-overlay {
  pointer-events: auto;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  background: rgba(51,51,51,0.5);
  z-index: 100;

  .modal-isshow {
    width: 70%;
    box-shadow: none;
    .modal-container {
      padding: 24px;
      margin: 0 auto;
      border-radius: 5px;
      background-color: #fff;
      position: relative;

      .alert-last-date {
        margin: 16px;
      }

      .close-btn {
        position: absolute;
        top: 5px;
        right: 10px;
      }

      .modal-heading {
        margin-bottom: 24px;
        color: #2c3e50;
        font-size: 16px;
      }
    }
  }
}
</style>
