<script setup>
import { ref, computed } from 'vue';
import { nanoid } from "nanoid";
import ToDoItem from './components/ToDoItem.vue';
import ToDoForm from './components/ToDoForm.vue';

// 定义响应式数据 ToDoItems
const ToDoItems = ref([
  { id: "todo-" + nanoid(), label: "Learn Vue", done: false },
  {
    id: "todo-" + nanoid(),
    label: "Create a Vue project with the CLI",
    done: true,
  },
  { id: "todo-" + nanoid(), label: "Have fun", done: true },
  {
    id: "todo-" + nanoid(),
    label: "Create a to-do list",
    done: false,
  },
]);

// 定义 addToDo 方法
const addToDo = (toDoLabel) => {
  ToDoItems.value.push({id: "todo-" + nanoid(), label: toDoLabel, done: false});
};

const updateDoneStatus = (toDoId) => {
  const toDoToUpdate = ToDoItems.value.find((item) => item.id === toDoId);
  toDoToUpdate.done = !toDoToUpdate.done;
};

// 定义计算属性：待办事项统计摘要
const listSummary = computed(()=> {
    const numberFinishedItems = ToDoItems.value.filter((item)=>item.done).length;
    return `${numberFinishedItems} out of ${ToDoItems.value.length} items completed`;
});
</script>

<template>
    <div id="app">
      <h1>To-do List</h1>
      <to-do-form @todo-added="addToDo"></to-do-form>
      <h2 id="list-summary">{{ listSummary }}</h2>
      <ul aria-labelledby="list-summary" class="stack-large">
        <li v-for="item in ToDoItems" :key="item.id">
          <to-do-item
          :label="item.label"
          :done="item.done"
          :id="item.id"
          @checkbox-changed="updateDoneStatus(item.id)"></to-do-item>
        </li>
      </ul>
    </div>
</template>

<style>
  /* 全局样式 */
  .btn {
    padding: 0.8rem 1rem 0.7rem;
    border: 0.2rem solid #4d4d4d;
    cursor: pointer;
    text-transform: capitalize;
  }
  .btn__danger {
    color: #fff;
    background-color: #ca3c3c;
    border-color: #bd2130;
  }
  .btn__filter {
    border-color: lightgrey;
  }
  .btn__danger:focus {
    outline-color: #c82333;
  }
  .btn__primary {
    color: #fff;
    background-color: #000;
  }
  .btn-group {
    display: flex;
    justify-content: space-between;
  }
  .btn-group > * {
    flex: 1 1 auto;
  }
  .btn-group > * + * {
    margin-left: 0.8rem;
  }
  .label-wrapper {
    margin: 0;
    flex: 0 0 100%;
    text-align: center;
  }
  [class*="__lg"] {
    display: inline-block;
    width: 100%;
    font-size: 1.9rem;
  }
  [class*="__lg"]:not(:last-child) {
    margin-bottom: 1rem;
  }
  @media screen and (min-width: 620px) {
    [class*="__lg"] {
      font-size: 2.4rem;
    }
  }
  .visually-hidden {
    position: absolute;
    height: 1px;
    width: 1px;
    overflow: hidden;
    clip: rect(1px 1px 1px 1px);
    clip: rect(1px, 1px, 1px, 1px);
    clip-path: rect(1px, 1px, 1px, 1px);
    white-space: nowrap;
  }
  [class*="stack"] > * {
    margin-top: 0;
    margin-bottom: 0;
  }
  .stack-small > * + * {
    margin-top: 1.25rem;
  }
  .stack-large > * + * {
    margin-top: 2.5rem;
  }
  @media screen and (min-width: 550px) {
    .stack-small > * + * {
      margin-top: 1.4rem;
    }
    .stack-large > * + * {
      margin-top: 2.8rem;
    }
  }
  /* 全局样式结束 */
  #app {
    background: #fff;
    margin: 2rem 0 4rem 0;
    padding: 1rem;
    padding-top: 0;
    position: relative;
    box-shadow:
      0 2px 4px 0 rgba(0, 0, 0, 0.2),
      0 2.5rem 5rem 0 rgba(0, 0, 0, 0.1);
  }
  @media screen and (min-width: 550px) {
    #app {
      padding: 4rem;
    }
  }
  #app > * {
    max-width: 50rem;
    margin-left: auto;
    margin-right: auto;
  }
  #app > form {
    max-width: 100%;
  }
  #app h1 {
    display: block;
    min-width: 100%;
    width: 100%;
    text-align: center;
    margin: 0;
    margin-bottom: 1rem;
  }
</style>


<!-- <style scoped>
/*<style> 标签上使用 scoped 属性可以把样式的作用范围限制在当前组件内。*/
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style> -->
