<template>
  <section class="todo">
    <div class="card bg-white shadow-xl m-6 border rounded-md p-5">
      <div class="m-3 text-xl">Todo List</div>
      <div
        class="todolist flex justify-between border rounded-md m-3"
        :class="{
          'border-green-500 bg-green-300': todo.isDone,
          'border-yellow-500 bg-yellow-100': todo.isPending,
        }"
        v-for="(todo, index) in todoList"
        :key="index"
      >
        <div class="content flex m-3 gap-8">
          <input
            class="checkbox accent-green-700"
            type="checkbox"
            v-model="todo.isDone"
            :disabled="todo.isPending"
          />
          <div class="todo__content">{{ todo.todo }}</div>
        </div>
        <!-- status -->
        <!-- Tombol selesai && tombol pending -->
        <!-- jika tombol selesai di klik, maka border akan berwarna hijau -->
        <!-- jika tombol pending di klik, maka border akan berwarna kuning -->
        <div class="status">
          <button
            class="pending py-2 px-2 m-2 bg-yellow-300 rounded-md hover:bg-yellow-400"
            @click.prevent="todoPending(todo)"
            :class="{
              hidden: todo.isDone,
            }"
          >
            Pending
          </button>
          <button
            class="hapus py-2 px-2 m-2 bg-red-500 hover:bg-red-600 rounded-md"
            @click.prevent="deleteTodo(todo)"
          >
            Hapus
          </button>
        </div>
      </div>
      <form action="#">
        <input
          class="todo border border-black rounded-md py-2 px-8 m-3"
          type="text"
          v-model="newTodo"
          placeholder="Enter a new todo"
        />
        <button @click.prevent="addTodo" class="py-2 px-2 m-2 bg-blue-500 rounded-md">Enter</button>
      </form>
    </div>
  </section>
</template>
<script>
export default {
  data() {
    return {
      newTodo: '',
      todoList: [
        {
          todo: 'Belajar Vue',
          status: 'pendding',
        },
        {
          todo: 'Belajar javascript',
          status: 'pendding',
        },
      ],
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() !== '') {
        this.todoList.push({
          todo: this.newTodo,
        })
        this.newTodo = ''
      }
    },
    deleteTodo(todo) {
      const index = this.todoList.indexOf(todo)
      this.todoList.splice(index, 1)
    },
    doneTodo(todo) {
      todo.isDone = !todo.isDone
    },
    todoPending(todo) {
      todo.isPending = !todo.isPending
    },
  },
}
</script>
