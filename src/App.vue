<template>
  <div id="app">
    <header>Todo List</header>
    <add-task></add-task>
  </div>
</template>

<script>
import AddTask from './components/AddTask'
export default {
  name: 'app',
  components: { AddTask }
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
}
</style>
