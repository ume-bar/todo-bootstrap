<template>
  <div class="container">
    <section class="todo-new">
      <h1>ToDoリスト</h1>
      <input v-model="todoItem.title" type="text" placeholder="todoを記入" />
      <button @click="addTodo()">Todoを追加</button>
    </section>

    <section class="todo-index">
      <h1>Incomplete todos</h1>
      <ul>
        <li v-for="(todo, i) in todoList" :key="i">
          <input
            class="item"
            type="checkbox"
            :checked="todo.isDone"
            @change="completeTodo(todo)"
          />
          <input
            class="item"
            type="text"
            v-model="todo.title"
            @change="updateTodo(i, todo)"
          />
          <button @click="deleteTodo(todo.id)">削除する</button>
        </li>
      </ul>
    </section>

    <section class="todo-complete">
      <h1>Complete todos</h1>
      <ul>
        <li v-for="(todo, i) in completeTodoList" :key="i">
          <input
            class="item"
            type="checkbox"
            :checked="todo.isDone"
            @change="completeTodo(todo)"
          />
          {{ todo.title }}
          <button @click="deleteTodo(todo.id)">削除する</button>
        </li>
      </ul>
    </section>
  </div>
</template>

<script lang="ts">
import {
  defineComponent,
  reactive,
  ref,
  onMounted,
} from "@nuxtjs/composition-api";
import { tutorial } from "../models/todo";
import $axios from "@nuxtjs/axios";

export default defineComponent({
  setup(_, { root }) {
    onMounted(() => {
      getTodo();
    });

    const todoItem = reactive({
      title: "",
      isDone: false,
    });

    const todoList = ref<tutorial[]>([]);
    const completeTodoList = ref<tutorial[]>([]);

    // todoをpost
    const addTodo = async () => {
      try {
        await root.$axios.post("/tutorials", {
          title: todoItem.title,
          isDone: todoItem.isDone,
        });
        getTodo();
        todoItem.title = "";
      } catch (e) {
        console.log(e);
      }
    };

    // todoをget
    const getTodo = async () => {
      try {
        const response = await root.$axios.get("/tutorials");
        todoList.value = { ...response.data.data };
        getCompleteTodo();
      } catch (e) {
        console.log(e);
      }
    };

    // todoをupdate
    const updateTodo = async (i: number, todo: tutorial) => {
      try {
        const newTodo = todoList.value[i].title;
        await root.$axios.patch(`/tutorials/${todo.id}`, { title: newTodo });
      } catch (e) {
        console.log(e);
      }
    };

    // todoをdelete
    const deleteTodo = async (id: number) => {
      try {
        await root.$axios.delete(`/tutorials/${id}`);
        getTodo();
      } catch (e) {
        console.log(e);
      }
    };

    // // todoをdone
    // const completeTodo = async (todo: tutorial) => {
    //   try {
    //     todo.isDone = !todo.isDone;
    //     await root.$axios.patch(`/tutorials/${todo.id}`, {
    //       isDone: todo.isDone,
    //     });
    //     getTodo();
    //   } catch (e) {
    //     console.log(e);
    //   }
    // };

    // complete_todoをget
    const getCompleteTodo = async () => {
      try {
        const response = await root.$axios.get("/tutorials/complete");
        completeTodoList.value = { ...response.data.data };
      } catch (e) {
        console.log(e);
      }
    };

    return {
      todoItem,
      todoList,
      completeTodoList,
      addTodo,
      deleteTodo,
      updateTodo,
      // completeTodo,
    };
  },
});
</script>



<style>

</style>