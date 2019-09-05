<template>
  <div id="app" class="container">
    <img src="./assets/logo.png" class="logo">
    <div class="input-container">
      <input type="text" v-model="todo" :class="[todo.length < 1 ? 'disabled' : 'enabled']" @keyup.enter="addTodo()">
      <i class="icon ion-ios-return-left" :class="[todo.length < 1 ? 'disabled-enter' : 'enabled']" @click="addTodo()"></i>
    </div>
    <ul class="todo-lists" v-for="todo in todos" :key="todo.id">
      <li>
        <div class="todo-item">
          <input type="checkbox" @click="completed(todo)">
          <p class="lead" :class="{completed: todo.completed}">{{todo.title}}</p>
          <i class="icon ion-ios-close" @click="removeTodo(todo)"></i>
        </div>
      </li>
    </ul>
    {{todos}}
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      todo: '',
      todos: [],
      id: 1
    }
  },
  methods: {
    addTodo() {
      if (this.todo.trim().length > 0) {
        this.todos.push({
          "id": this.id,
          "title": this.todo,
          "completed": false,
          "editing": false
        });
        this.id++;
        this.todo = '';
      }
    },
    completed(todo) {
      todo.completed = !todo.completed
    },
    removeTodo(todo) {
      var index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
    }
  }
}
</script>

<style lang="scss">

.container {
  max-width: 600px;
  margin: 0 auto;
  .todo-lists {
    list-style: none;
    display: flex;
    width: calc(100% - 20%);
    vertical-align: center;
    margin: 0 auto;
    border: 1px solid gray;

      .todo-item {
        .icon {
          font-size: 25px;
          vertical-align: center;
          display: inline-block;
          color: #EC407A;
        }

        .lead {
          display: inline-block;
          margin: auto 0;
        }

        .completed {
          color: #EC407A;
        }
      }
    }

  .input-container {
    margin-top: 35px;
    display: flex;
    width: 100%;
    // border: 1px solid gray;
    input {
      width: 100%;
      font-size: 18px;
      padding: 8px 20px;
      border-top-left-radius: 2rem;
      border-bottom-left-radius: 2rem;
      border-top: 1px solid gray;
      border-left: 1px solid gray;
      border-bottom: 1px solid gray;
      transition: all 0.5s;
      border-right: none;
        &:focus {
          outline: none;
        }
    }
    i {
      font-size: 35px;
      border-top: 1px solid gray;
      border-right: 1px solid gray;
      border-bottom: 1px solid gray;
      border-left: none;
      color: gray;
      border-top-right-radius: 2rem;
      border-bottom-right-radius: 2rem;
      padding: 0 15px;
      transition: all 0.4s;
      
    }
    .disabled {
      border-top: 1px solid #EC407A;
      border-left: 1px solid #EC407A;
      border-bottom: 1px solid #EC407A;
    }

    .disabled-enter {
      border-top: 1px solid #EC407A;
      border-right: 1px solid #EC407A;
      border-bottom: 1px solid #EC407A;
      color: #EC407A;
    }

  }
}

.logo {
  width: 120px;
  display: block;
  margin: 0 auto;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  // text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
