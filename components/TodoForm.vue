<template>
  <b-container>
    <b-input-group>
      <!-- v-model属性で双方向ディバイディング -->
      <b-form-input type="text" v-model="value"/>
      <b-input-group-append>
        <b-button variant="primary" @click="handleAddTodo()">追加</b-button>
      </b-input-group-append>
    </b-input-group>
  </b-container>
</template>

<script>
export default {
  name: 'TodoForm',
  data () {
    return {
      value: ''
    }
  },
  methods: {
    // 送信ボタンクリック時に処理される関数
    handleAddTodo () {
      // Index.vueのhandleParentAddTodoにフォーム内の値を引数に発火
      this.$emit('handleParentAddTodo', this.value)
      this.value = ''
    }
  }

}
</script>

<style>

</style>
