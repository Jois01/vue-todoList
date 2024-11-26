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
            class="pending md:py-2 md:px-2 p-1 m-2 bg-yellow-300 rounded-md hover:bg-yellow-400"
            @click.prevent="todoPending(todo)"
            :class="{
              hidden: todo.isDone,
            }"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
              class="size-4 md:size-6"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M16.023 9.348h4.992v-.001M2.985 19.644v-4.992m0 0h4.992m-4.993 0 3.181 3.183a8.25 8.25 0 0 0 13.803-3.7M4.031 9.865a8.25 8.25 0 0 1 13.803-3.7l3.181 3.182m0-4.991v4.99"
              />
            </svg>
          </button>
          <button
            class="hapus md:py-2 md:px-2 p-1 m-2 bg-red-500 rounded-md hover:bg-red-600"
            @click.prevent="deleteTodo(todo)"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
              class="size-4 md:size-6 stroke-white"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="m14.74 9-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 0 1-2.244 2.077H8.084a2.25 2.25 0 0 1-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 0 0-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 0 1 3.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 0 0-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 0 0-7.5 0"
              />
            </svg>
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
