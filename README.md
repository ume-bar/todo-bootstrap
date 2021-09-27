# todo-bootstrap

## Build Setup

```bash
# install dependencies
$ yarn install

# serve with hot reload at localhost:3000
$ yarn dev

# build for production and launch server
$ yarn build
$ yarn start

# generate static project
$ yarn generate
```

For detailed explanation on how things work, check out the [documentation](https://nuxtjs.org).

## Special Directories

You can create the following extra directories, some of which have special behaviors. Only `pages` is required; you can delete them if you don't want to use their functionality.

### `assets`

The assets directory contains your uncompiled assets such as Stylus or Sass files, images, or fonts.

More information about the usage of this directory in [the documentation](https://nuxtjs.org/docs/2.x/directory-structure/assets).

### `components`

The components directory contains your Vue.js components. Components make up the different parts of your page and can be reused and imported into your pages, layouts and even other components.

More information about the usage of this directory in [the documentation](https://nuxtjs.org/docs/2.x/directory-structure/components).

### `layouts`

Layouts are a great help when you want to change the look and feel of your Nuxt app, whether you want to include a sidebar or have distinct layouts for mobile and desktop.

More information about the usage of this directory in [the documentation](https://nuxtjs.org/docs/2.x/directory-structure/layouts).


### `pages`

This directory contains your application views and routes. Nuxt will read all the `*.vue` files inside this directory and setup Vue Router automatically.

More information about the usage of this directory in [the documentation](https://nuxtjs.org/docs/2.x/get-started/routing).

### `plugins`

The plugins directory contains JavaScript plugins that you want to run before instantiating the root Vue.js Application. This is the place to add Vue plugins and to inject functions or constants. Every time you need to use `Vue.use()`, you should create a file in `plugins/` and add its path to plugins in `nuxt.config.js`.

More information about the usage of this directory in [the documentation](https://nuxtjs.org/docs/2.x/directory-structure/plugins).

### `static`

This directory contains your static files. Each file inside this directory is mapped to `/`.

Example: `/static/robots.txt` is mapped as `/robots.txt`.

More information about the usage of this directory in [the documentation](https://nuxtjs.org/docs/2.x/directory-structure/static).

### `store`

This directory contains your Vuex store files. Creating a file in this directory automatically activates Vuex.

More information about the usage of this directory in [the documentation](https://nuxtjs.org/docs/2.x/directory-structure/store).


<template>
  <div id="Todo">
    <h1>ToDoリスト</h1>
    <todo-form @handleParentAddTodo="handleParentAddTodo" />
    <todo-list
      :todos="todos"
      @handleParentDeleteTodo="handleParentDeleteTodo"
      @handleParentCompleteTodo="handleParentCompleteTodo" />
  </div>
</template>

<script>
// TodoForm,TodoList読み込み
import TodoForm from '@/components/TodoForm'
import TodoList from '@/components/TodoList'
import axios from './axios'

export default {
  name: 'Todo',
  components: {
    TodoForm,
    TodoList
  },
  data () {
    return {
      // データバインディング
      todos: []
    }
  },
  methods: {
    // v-onでメソッド呼び出し
    // Todoリスト追加処理
    async handleParentAddTodo (value) {
      if (value) {
        // メモを投稿するAPIを実行
        await axios.post("/tutorials", {

        })
        // メモの一覧を取得するAPIを実行
        this.todos = await axios.get("/tutorials")
      }}
    },
    // Todoリスト完了処理
    // この処理でcompleteの真偽を逆転させる
    handleParentCompleteTodo (index) {
      // this.todos[index].complete = !this.todos[index].complete
    },
    // Todoリスト削除処理
    // spliceで引数の一行を消去
    handleParentDeleteTodo (index) {
      app.post('/delete/:id', (req, res) => {
  client.query(
    'DELETE FROM items WHERE id=?',
    [req.params.id],
    (error, results) => {
      res.redirect('/index');
    }
  );
});
      // this.todos.splice(index, 1)
    }
  }

</script>

<style>

</style>