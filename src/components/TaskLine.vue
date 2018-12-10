<template>
  <li class="line task">
    <div v-bind:class="{ strike: task.done }">{{ task.text }}</div>
    <button v-if="task.done" class="delete"v-on:click="deleteTask">
      Effacer
    </button>
    <button class="done" v-on:click="toggle">
      {{ task.done ? 'A terminer' : 'Terminé' }}
    </button>
  </li>
</template>

<script>
export default {
  name: 'TaskLine',
  props: [ 'task' ],
  methods: {
    toggle () {
      this.$emit('toggle')
    },
    deleteTask () {
      this.$emit('delete')
    }
  }
}
</script>

<style lang="scss" scoped>
.task {
  line-height: 24px;
  div {
    flex: 1;
    text-align: left;
  }
}
.done {
  width: 80px;
  font-size: 10px;
  padding: 4px !important;
  background-color: darkgreen !important;
}
.delete {
  width: 80px;
  font-size: 10px;
  padding: 4px !important;
  background-color: darkred !important;
  margin-right: 16px;
}
.strike {
  text-decoration: line-through;
  opacity: 0.75;
}
</style>
