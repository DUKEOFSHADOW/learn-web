<script setup>
import ToDoItem from './components/ToDoItem.vue';
import { nanoid } from "nanoid";

// 组件名称可以通过文件名推断，或者在构建工具中配置
// components 选项不再需要，因为在 <script setup> 中导入的组件会自动注册
// data 选项中的响应式数据可以直接使用 ref 或 reactive 定义
const ToDoItems = [
        { id: "todo-" + nanoid(),
          label: "Learn Vue",
          done: false,
        },
        {
          id: "todo-" + nanoid(),
          label: "Create a Vue project with the CLI",
          done: true,
        },
        { id: "todo-" + nanoid(),
          label: "Have fun",
          done: true,
        },
        {
          id: "todo-" + nanoid(),
          label: "Create a to-do list",
          done: false,
        },
];

</script>

<template>
    <div id="app">
      <h1>To-do List</h1>
      <ul>
        <li v-for="item in ToDoItems" :key="item.id">
          <to-do-item :label="item.label" :done="item.done" :id="item.id"></to-do-item>
        </li>
      </ul>
    </div>

</template>

<!-- <style scoped>
/*scoped属性将样式的范围限制到单个文件组件的内容里*/
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
