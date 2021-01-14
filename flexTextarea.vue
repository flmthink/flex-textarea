<template>
  <div class="wrapper textarea-wrapper">
    <div class="content-editable"
         :style="customStyle"
         contenteditable="true" v-text="value">
        </div>
    <textarea v-if="progress"
              class="content-mask"
              :style="customStyle"
              readonly
              :value="contentValueDone">
              </textarea>
    <textarea class="field-textarea"
              :style="customStyle"
              :placeholder="placeholder"
              :readonly="readonly"
              :value="value"
              @input="emit2father">
              </textarea>
  </div>
</template>

<script>
export default {
  name: 'flexTextarea',
  props: {
    value: [String, Number],
    placeholder: [String, Number],
    readonly: Boolean,
    customStyle: Object,
    progress: Boolean,
    progressIndex: Number
  },
  computed: {
    contentValueDone () {
      return String(this.value).substring(0, this.progressIndex)
    }
  },
  methods: {
    emit2father (e) {
      this.$emit('input', e.target.value)
    }
  }
}
</script>

<style lang="stylus" scoped>
*
  color inherit
  font-size inherit
  font-weight inherit
  font-family inherit
  font-style inherit
  text-indent inherit
  text-align inherit
  line-height inherit
  word-spacing inherit
  letter-spacing inherit
  text-transform inherit
  visibility inherit
  cursor inherit
  word-break break-all
  box-sizing border-box
.textarea-wrapper
  position relative
  display block
  width 100%
.content-editable
  position relative
  z-index -1
  opacity 0
  display block
  width 100%
  white-space: pre-wrap; // 与textarea默认一致
.content-mask,.field-textarea
  resize none
  position absolute
  top 0
  left 0
  width 100%
  height 100%
  text-align left
  overflow hidden
.content-mask
  background-color transparent !important
  z-index 1
  pointer-events none
  color #67C23A
.field-textarea
  background-color transparent
.field-textarea::-webkit-input-placeholder
  text-align left

</style>
