<template>
  <div id="app">
    <header>Todo List</header>
    <add-task v-on:input="addTask"></add-task>
    <ul class="list">
      <task-line v-for="task in sortedTasks"
                 v-bind:key="`task_${task.created}`"
                 v-bind:task="task"
                 v-on:toggle="toggleTask(task.created)"
                 v-on:edit="editTask(task.created)"
                 v-on:delete="deleteTask(task.created)"></task-line>
    </ul>
    <task-editor v-if="editedTask !== undefined"
                 v-on:modify="modifyTask"
                 v-on:cancel="cancelEdit"
                 v-bind:task="tasks[editedTask]"></task-editor>
  </div>
</template>

<script>
import AddTask from './components/AddTask'
import TaskLine from './components/TaskLine'
import TaskEditor from './components/TaskEditor'
export default {
  name: 'app',
  components: { AddTask, TaskLine, TaskEditor },
  data () {
    return {
      tasks: [],
      editedTask: undefined
    }
  },
  computed: {
    sortedTasks () {
      const tasks = this.tasks
      return tasks.sort((a, b) => {
        if (a.done && !b.done) return 1
        if (!a.done && b.done) return -1
        return a.created - b.created
      })
    }
  },
  methods: {
    addTask (taskText) {
      this.tasks.push({
        text: taskText,
        created: Date.now(),
        done: false
      })
      this.saveTasks()
    },
    index (created) {
      for (let i = 0; i < this.tasks.length; i++) {
        if (this.tasks[i].created === created) return i
      }
      return -1
    },
    toggleTask (created) {
      const i = this.index(created)
      this.tasks[i].done = !this.tasks[i].done
      this.saveTasks()
    },
    deleteTask (created) {
      this.tasks.splice(this.index(created), 1)
      this.saveTasks()
    },
    editTask (created) {
      this.editedTask = this.index(created)
    },
    modifyTask (task) {
      this.tasks[this.editedTask] = task
      this.editedTask = undefined
      this.saveTasks()
    },
    cancelEdit () {
      this.editedTask = undefined
    },
    saveTasks () {
      localStorage.setItem('tasks', JSON.stringify(this.tasks))
    },
    restoreTasks () {
      const stor = localStorage.getItem('tasks')
      if (stor) this.tasks = JSON.parse(stor)
    }
  },
  mounted () {
    this.restoreTasks()
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
