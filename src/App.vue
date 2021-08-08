<template>
  <div>
    <h1> Input Value: {{inputValue}} </h1>

<!--    <input type="text" :value="inputValue" @input="handleInputChange"/>-->
<!--    <input type="text" :value="inputValue" @input="inputValue = $event.target.value"/>-->
    <input type="text" v-model.trim="inputValue"  @keypress.enter="createNewTodo"/>

    <button @click="createNewTodo">create todo</button>
<!--    <br>-->
<!--    <input type="checkbox" v-model="isOn"/>-->
<!--    <br>-->
<!--    <button @click="isOn = !isOn">toggle checkbox</button>-->

    <div v-if="todo">{{todo.id}}  - {{todo.title}} - {{todo.completed}} </div>

    <ul v-if="todos.length">
      <li v-for="todo of todos" :key="todo.id" @click="selectedTodoId = todo.id">{{todo.id}}  - {{todo.title}} - {{todo.completed}}    </li>
    </ul>
    <h2 v-else-if="loading"> LOADING </h2>
    <h2 v-else> NO DATA </h2>
  </div>

  <div v-for="error of errors" :key="error"> {{error}}  </div>

</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      isOn: false,
      inputValue: '',
      todos: [],
      todo: null,
      selectedTodoId: null,
      loading: false

    }
  },
  methods: {
    // alertHandler() {
    //   alert('hello');
    // },
    // handleInputChange(e) {
    //   const { target: {value} } = e;
    //
    //   if(value.length >= 5) {
    //     e.preventDefault()
    //   }
    // }
    createNewTodo() {

      if(!this.inputValue) return;

      const newTodo = {
        id: Math.random(),
        title: this.inputValue,
        completed: false
      }

      this.todos.unshift(newTodo);
      this.inputValue = '';


    },
    async fetchTodos() {
      try {
        this.loading = true;
        const res= await fetch('https://jsonplaceholder.typicode.com/todos');
        this.todos = await res.json();

      } catch (e) {
        console.log(e)
      } finally {
        this.loading = false
      }

    },

    async fetchTodo(id) {
      try {
        this.loading = true;
        const res= await fetch(`https://jsonplaceholder.typicode.com/todos/${id}`);
        this.todo = await res.json();

      } catch (e) {
        console.log(e)
      } finally {
        this.loading = false
      }

    }

  },

  watch: {
    selectedTodoId() {
      this.fetchTodo(this.selectedTodoId)
    }
  },

  //lifecycle


  created() {
    this.fetchTodos()
  }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
