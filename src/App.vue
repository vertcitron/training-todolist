<template>
  <div id="app">
    <header>Todo List</header>
    <add-task v-on:input="addTask"></add-task>
    <ul class="list">
      <task-line v-for="(task, i) in tasks"
                 v-bind:key="`task_${i}`"
                 v-bind:task="task"
                 v-on:toggle="toggleTask(i)"></task-line>
    </ul>
  </div>
</template>

<script>
import AddTask from './components/AddTask'
import TaskLine from './components/TaskLine'
export default {
  name: 'app',
  components: { AddTask, TaskLine },
  data () {
    return {
      tasks: []
    }
  },
  methods: {
    addTask (taskText) {
      this.tasks.push({
        text: taskText,
        created: Date.now(),
        done: false
      })
    },
    toggleTask (i) {
      this.tasks[i].done = !this.tasks[i].done
    }
  }
}
</script>

<style lang="scss">
body {
  background-color: #888;
  height: 100%;
  font-family: sans-serif;
}
#app {
  text-align: center;
  background-color: #fafafa;
  color: #444;
  margin: 60px auto 48px auto;
  width: 75%;
  border-radius: 6px;
  padding: 12px;
  box-shadow: 2px 2px 6px rgba(black, 0.33);
  header {
    font-size: 24px;
    font-weight: bold;
    border-bottom: 1px solid #888;
    padding-bottom: 12px;
  }
  .line {
    margin-left: auto;
    margin-right: auto;
    width: 75%;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
  }
  button {
    border: none;
    padding: 8px 16px;
    border-radius: 6px;
    box-shadow: 2px 2px 8px rgba(black, 0.33);
    background-color: #4682b4;
    color: white;
    font-weight: bold;
    opacity: 0.85;
    &:hover {
      opacity: 1;
      cursor: pointer;
      box-shadow: 2px 2px 8px rgba(black, 0.5);
    }
  }
  input[type=text] {
    line-height: 24px;
    border: none;
    border-bottom: 1px solid #888;
    background-color: inherit;
    &:focus {
      background-color: white;
    }
  }
  ul.list {
    margin-top: 20px;
    margin-bottom: 20px;
    padding: 0;
  }
}
::placeholder {
  color: #444;
  opacity: 0.5;
}
</style>
