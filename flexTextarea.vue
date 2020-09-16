<template>
  <div class="wrapper textarea-wrapper">
    <div class="content-editable"
         contenteditable="true" v-html="contentValue"></div>
    <textarea class="field-textarea"
              :placeholder="placeholder"
              :value="value"
              @input="emit2father">
              </textarea>
  </div>
</template>

<script>
export default {
  name: 'flexTextarea',
  props: {
    placeholder: String,
    value: String
  },
  computed: {
    contentValue () {
      return this.value.replace(/\n/g, '<br> ') + '<br>' // div中文字末尾加一个<br>并不能起到另起一行的作用，需要后面再添加内容，两个<br>则可以直接另起一行
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
  // white-space pre
.field-textarea
  position absolute
  top 0
  left 0
  width 100%
  height 100%
  box-sizing border-box
  text-align left
  resize none
  overflow hidden
  background-color transparent
.field-textarea::-webkit-input-placeholder
  text-align left
</style>
