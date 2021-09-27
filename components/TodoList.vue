<template>
  <b-container>
    <!-- for文でTodoリストをひとつづつ処理 -->
    <b-row :key="index" v-for="(todo, index) in todos" class="mt-2">
      <!-- v-bindのclass属性によりcomplete時にstyleが適用 -->
      <b-col cols="8" :class="[{line: todo.complete}, 'text-left']">
        <h5>{{todo.text}}</h5>
      </b-col>
      <b-col cols="4" class="text-right">
        <b-button @click="handleCompleteTodo(index)"
        :variant="todo.complete ? '' : 'success'">
          {{ todo.complete ? '完了' : '未完了'}}
          </b-button>
        <b-button @click="handleDeleteTodo(index)" variant="danger">削除</b-button>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
export default {
  name: 'TodoList',
  // 親コンポーネントからv-bindで渡された値（todos）を受け取る
  props: ['todos'],
  methods: {
    // 完了ボタンクリック時に処理される関数
    handleCompleteTodo (index) {
      // Index.vueのhandleParentCompleteTodoにフォーム内の値を引数に発火
      this.$emit('handleParentCompleteTodo', index)
    },
    // 削除ボタンクリック時に処理される関数
    handleDeleteTodo (index) {
      // Index.vueのhandleParentDeleteTodoにフォーム内の値を引数に発火
      this.$emit('handleParentDeleteTodo', index)
    }
  }
}
</script>

<style scoped>
  .line {
    text-decoration: line-through;
  }
</style>
