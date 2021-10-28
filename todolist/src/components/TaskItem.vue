<template>
  <div>
    <li class="task_item" :class="{complete: task.completed}">
      <input type="button" class="task_complete" @click="taskComplete(task)"  value="√">
      <span class="task_content">{{task.content}}</span>
      <input type="button" class="tomato" value="">
      <button class="delete" @click="taskDelete(task)">×</button>
    </li>
  </div>
</template>

<script>
export default {
  name: 'TaskItem',
  // 当前task对象，调用task完成的父组件方法，调用task删除的父组件方法
  props: ['task', 'taskComplete', 'taskDelete'],
}
</script>

<style scoped>
    li:hover {
        background-color: #f0f0f0;
    }

    .task_item {
        position: relative;
        padding: 14px 20px 15px;
        border-bottom: 1px solid #e6e6e6;
    }

    .task_complete {
        float: left;
        margin-left: 5px;
        width: 17px;
        height: 17px;
        color: white;
        background-color: white;
        border: 1px solid rgb(179, 172, 172);
        border-radius: 50%;
    }

    .task_content {
        float: left;
        font-weight: bold;
        margin-left: 15px;
    }

/* task completed */
    .complete {
        color: #b5b5b5;
    }

    .complete .task_complete {
        background-color: #ec7260;
    }

    .complete .task_content {
        text-decoration: line-through;
    }

/* task delete */
    .delete {
        visibility: hidden;
        float: right;
        width: 20px;
        height: 20px;
        border-radius: 50%;
        color: rgb(184, 184, 184);
        background-color: white;
        cursor: pointer;
    }

    .task_item:hover .delete {
        visibility: visible;
    }
</style>
