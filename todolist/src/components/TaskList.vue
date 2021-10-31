<template>
  <div id="task_list">
      <ul class="tsklist_underway">
        <TaskItem 
          v-for="taskObj in tasks"
          :key="taskObj.id"
          :taskComplete="taskComplete"
          :task="taskObj"
          :taskDelete="taskDelete"
          :changeTask="changeTask"
        />
      </ul>
  </div>
</template>

<script>
import TaskItem from './TaskItem.vue'

export default {
  name: 'TaskList',
  components: {TaskItem},
  props: ['tasks', 'taskComplete', 'taskDelete', 'changeTask']
}
</script>


<style scoped>
  /* tasks list */
  #task_list {
      margin-top: 10px;
      width: 100%;
      height: 600px;
  }
</style>
