<template>
  <div>
    <div id="ap">
        <main>
            <div class="header">
              <AddItem :addTask="addTask"/>
              <NowT/>
            </div>
            <TaskList :tasks="tasks" :taskComplete="taskComplete" :taskDelete="taskDelete" />
            <div class="footer">
              <TaskTools :tasks="tasks" :checkAll="checkAll" :clearAllTask="clearAllTask"/>
            </div>
        </main>
    </div>
    
  </div>
</template>

<script>
import AddItem from './components/AddItem.vue'
import TaskList from './components/TaskList.vue'
import TaskTools from './components/TaskTools.vue'
import NowT from './components/NowT.vue'


export default {
  name: 'App',
  components: {AddItem, TaskList, TaskTools, NowT},
  data() {
    return {
      tasks: [
        {id:'001', content:'吃饭', completed: false},
        {id:'002', content:'睡觉', completed: true},
        {id:'003', content:'打游戏！', completed: false}
      ]
    }
  },
  methods: {
      addTask(taskObj) {
        // 将新的task对象假如tasks数组
        this.tasks.unshift(taskObj);
      },
      taskComplete(taskObj) {
        // 被点击的task对象completed值取反
        taskObj.completed = !taskObj.completed;
      },
      taskDelete(taskObj) {
        // 遍历tasks找到应该被删除的task，返回删除后的新数组
        this.tasks = this.tasks.filter(function(i) {
          return taskObj !== i
        })
      },
      checkAll(bool) {
        // 修改所有task的完成状态为bool
        this.tasks.forEach((item)=>{
          item.completed = bool;
        })
      },
      clearAllTask() {
        // 清除所有已经完成的任务
        this.tasks = this.tasks.filter(function(task) {
          return !task.completed
        })
      }
  }
}
</script>

<style>
  * {
      margin: 0;
      padding: 0;
      outline: none;
  }

  /* 字体图标通用 */
  .icon {
      width: 1em; height: 1em;
      vertical-align: -0.15em;
      fill: currentColor;
      overflow: hidden;
  }

  button {
      border: 1px solid transparent;
      outline: none;
  }

  li {
      list-style: none;
  }

  input {
      border: 0;
  }

  #ap {
      margin: 20px auto;
      width: 700px;
      height: 700px;
      border: 1.5px solid #ecdfdf;
      border-radius: 10px;
  }

  /* .header */
  .header {
    margin: 26px 25px 0;
    height: 70px;
  }

  /* footer */
  .footer {
    padding: 5px;
    overflow: hidden;
    border: 1px solid #ecdfdf;
    border-radius: 10px;
  }

</style>
