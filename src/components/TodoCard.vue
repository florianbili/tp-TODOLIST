<template>
  <section class="todoapp">
    <header class="header">
      <p>{{ date }}</p>
      <h1>VueJs Tutorial Todo List</h1>
      <span class="todo-count">{{ remaining }}Tâches</span>

      
    </header>
    <div class="main">
    <input
        type="text"
        class="new-todo"
        placeholder="Nouvelle tache"
        v-model="newTodo"
      />
     <button type="button" @click.prevent="addTodo">Ajouter</button>
    <ul class="todo-list">
      <li
        class="todo"
        v-bind:key="todo.name"
        v-for="todo in TodoCard" :class="{ completed: todo.completed }"
      >
        <div class="view">
          <input type="checkbox" v-model="todo.completed" class="toggle" />
          <label>{{ todo.name }}</label>
          <button type="button"  @click.prevent="deleteTodo(todo)">Supprimer</button> 
        </div>
       
      </li>
    </ul>
     </div>
  </section>
</template>

<script>

export default {
  data() {
    return {
      TodoCard: [
        {
          name: "Tache de test",
          completed: false,
        },
      ],
      newTodo: "",
    };
  },
  methods: {
    addTodo() {
      this.TodoCard.push({
        completed: false,
        name: this.newTodo,
      });
      this.newTodo = "";
    },
    deleteTodo(todo){
      this.TodoCard = this.TodoCard.filter(i => i !== todo)
    }
  },
  computed: {
    date: function () {       
      let current = new Date();       
      let jour = current.toLocaleString("default", { weekday: "long" });       
      let month = current.toLocaleString("default", { month: "long" });       
      let date = current.getDate();       let dateTime = jour + " " + date + " " + month;        
      return dateTime;     },
    remaining() {
      return this.TodoCard.filter((todo) => !todo.completed).length;
    },
  },
};
</script>

<style src="./TodoCard.css"></style>