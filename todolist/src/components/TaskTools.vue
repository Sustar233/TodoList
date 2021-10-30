<template>
  <div class="task_tools" v-show="allTask">
    <input type="button" class="task_complete" value="√" :class="{complete: isCheckAll}" @click="handleCheckAll">
    <h5 class="task_status">已完成 <span>{{done}}</span> / 全部 <span>{{allTask}}</span></h5>
    <button class="clearTask" @click="clearAllTask">清空已完成</button>
  </div>
</template>

<script>
export default {
  name: 'TaskTools',
  props: ["tasks"],
  data() {
    return {
      isCheckAll: false
    }
  },
  methods: {
    // 点击全选时，对全选值取反
    handleCheckAll() {
      this.isCheckAll = !this.isCheckAll;
      this.$emit('receiveCheckAll', this.isCheckAll);
    },
    // 点击按钮时，清除所有已完成的任务
    clearAllTask() {
      this.$emit('clearAllTask')
    }
  },
  computed: {
    // 遍历tasks，统计completed任务的数量
    done() {
      return this.tasks.reduce((pre,task) => {
        return pre + (task.completed ? 1 : 0);
      }, 0)
    },
    // 一共有多少任务
    allTask() {
      return this.tasks.length
    }
  },
  watch: {
    // 监听已完成任务数，当已完成任务=所有任务时勾选全选按钮
    done() {
      if (this.done === this.allTask && this.done !== 0) {
        this.isCheckAll = true;
      } else {
        this.isCheckAll = false;
      }
    }
  }
}
</script>


<style scoped>
  .task_complete {
    float: left;
    margin-left: 20px;
    width: 17px;
    height: 17px;
    color: white;
    background-color: white;
    border: 1px solid rgb(179, 172, 172);
    border-radius: 50%;
  }

  .task_status {
    float: left;
    margin-left: 40px;
  }

  .clearTask {
    float: right;
    height: 17px;
    line-height: 17px;
    border-radius: 5px;
  }

  .clearTask:hover {
    background-color: #e4e2e2;
  }

  /* task completed */
  .complete {
    color: white;
    background-color: #ec7260;
  }
</style>
