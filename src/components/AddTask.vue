<template>
  <div class="line add-task">
    <input class="wide" type="text" placeholder="Nouvelle tâche" v-model="newTask" />
    <button @click="addTask">Ajouter</button>
  </div>
</template>

<script>
export default {
  name: 'AddTask',
  data () {
    return {
      newTask: ''
    }
  },
  methods: {
    addTask () {
      if (this.newTask) this.$emit('input', this.newTask)
      this.newTask = ''
    }
  }
}
</script>

<style lang="scss" scoped>
.add-task {
  margin-top: 20px;
  margin-bottom: 20px;
}
.wide {
  margin-right: 32px;
  flex: 1;
}
</style>
