<template>
  <div class="backdrop">
    <div class="editor">
      <h5>Modifier une tâche</h5>
      <input type="text"
             v-model="text"
             autofocus />
      <button class="okBtn" v-on:click="modifyTask">OK</button>
      <button class="cancelBtn" v-on:click="cancelEdit">Annuler</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TaskEditor',
  props: [ 'task' ],
  data () {
    return { text: '' }
  },
  methods: {
    modifyTask () {
      if (this.text) {
        this.$emit('modify', {
          text: this.text,
          created: this.task.created,
          done: this.task.done
        })
      }
    },
    cancelEdit () {
      this.$emit('cancel')
    }
  },
  mounted () {
    this.text = this.task.text
  }
}
</script>

<style lang="scss" scoped>
.backdrop {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(black, 0.5);
}
.editor {
  padding: 16px;
  width: 50%;
  margin: 150px auto;
  background-color: #fafafa;
  border-radius: 6px;
  box-shadow: 4px 4px 10px rgba(black, 0.5);
  input {
    display: block;
    margin: 0 auto 20px auto;
    width: 75%;
  }
  .okBtn {
    background-color: darkgreen !important;
    margin-right: 16px;
  }
  .cancelBtn {
    background-color: darkred !important;
  }
}
</style>
