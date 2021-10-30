<template>
  <div class="add_task">
    <input type="text" class="task_input" placeholder="添加事件" @keyup.enter="add">
  </div>
</template>

<script>
  import {nanoid} from 'nanoid'
  export default {
    name: 'AddItem',
    methods: {
      add(e) {
        // 校验数据
        if (!e.target.value.trim()) return alert('输入不能为空');
        // 将用户输入包装成一个task对象
        const taskObj = {id:nanoid(), content:e.target.value, completed: false};
        // 通知App组件去添加一个task对象
        this.$emit('receiveAddTask', taskObj);
        // 清空输出
        e.target.value = '';
      }
    }
  }
</script>


<style scoped>
  .task_input {
    float: left;
    padding: 8px 18px;
    width: 360px;
    height: 24px;
    color: #a1a1a1;
    background-color: #f7f7f7;
    border: 1px solid #b8b8b8;
    border-radius: 5px;
  }
</style>
