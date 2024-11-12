<template>
  <section class="todo">
    <div class="m-3 mt-8 text-xl">Todo List</div>
    <form action="#">
      <!-- kategori -->
      <!-- <input
        class="kategori border border-black rounded-md py-2 px-8 m-3"
        type="text"
        v-model="kategori"
        placeholder="masukkan kategori, misal:PR"
      /> -->
      <!-- todolistnya apa -->
      <input
        class="todo border border-black rounded-md py-2 px-8 m-3"
        type="text"
        v-model="newTodo"
        placeholder="Enter a new todo"
      />
      <button @click.prevent="addTodo" class="py-2 px-2 m-2 bg-blue-500 rounded-md">Enter</button>
    </form>
    <div class="card bg-white shadow-xl m-3 border rounded-md p-5">
      <div
        :class="['todolist flex justify-between border', `border-${status}`, 'rounded-md m-3']"
        v-for="(todo, index) in todoList"
        :key="index"
      >
        <div class="content flex m-3 gap-8">
          <input class="checkbox" type="checkbox" @click.prevent="doneTodo" />
          <!-- <div class="todo__kategori">{{ todo.kategori }}</div> -->
          <div class="todo__content">{{ todo.todo }}</div>
        </div>
        <!-- status -->
        <!-- Tombol selesai && tombol pending -->
        <!-- jika tombol selesai di klik, maka akan bepindah ke done -->
        <!-- jika tombol pending di klik, maka akan bepindah ke pending -->
        <div class="status">
          <button
            class="pending py-2 px-2 m-2 bg-yellow-300 rounded-md"
            @click.prevent="changeStatus"
          >
            Pending
          </button>
          <button class="hapus py-2 px-2 m-2 bg-red-500 rounded-md" @click.prevent="deleteTodo">
            Hapus
          </button>
        </div>
      </div>
    </div>
  </section>
</template>
<script>
export default {
  created() {
    this.getStatusSetting()
  },
  data() {
    return {
      kategori: '',
      newTodo: '',
      todoList: [
        {
          kategori: 'PR',
          todo: 'Belajar Vue',
          status: 'pendding',
        },
        {
          kategori: 'PR',
          todo: 'Belajar React',
          status: 'pendding',
        },
      ],
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() !== '') {
        this.todoList.push({
          kategori: this.kategori,
          todo: this.newTodo,
        })
        this.newTodo = ''
      }
    },

    deleteTodo(index) {
      this.todoList.splice(index, 1)
    },
    changeStatus() {
      let status = 'gray-600'
      if (this.status == 'gray-600') {
        status = 'yellow-500'
      }
      this.status = status
      this.storeStatusSetting()
    },
    storeStatusSetting() {
      localStorage.setItem('status', this.status)
    },
    getStatusSetting() {
      let status = localStorage.getItem('status')
      if (status) {
        this.status = status
      }
    },
    doneTodo(index) {
      this.todoList[index].status = 'done'
    },
  },
}
</script>
