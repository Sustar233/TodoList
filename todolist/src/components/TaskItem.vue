<template>
    <transition name="task" appear>
        <div>
            <li class="task_item" :class="{complete: task.completed}">
                <input type="button" class="task_complete" @click="taskComplete(task)"  value="√">
                <span 
                    class="task_content"
                    v-show="!isEdit"
                    @dblclick="handleEdit"
                >
                    {{task.content}}
                </span>

                <!-- 平时隐藏 -->
                <input 
                    type="text"
                    class="edit_content"
                    ref="inputContent"
                    v-show="isEdit"
                    :value="task.content"
                    @blur="handleEdit"
                >
                <button class="delete" @click="taskDelete(task)">×</button>
            </li>
        </div>    
    </transition>
</template>

<script>
    export default {
        name: 'TaskItem',
        // 当前task对象，调用task完成的父组件方法，调用task删除的父组件方法
        props: ['task', 'taskComplete', 'taskDelete', 'changeTask'],
        data() {
            return {
                isEdit: false
            }
        },
        methods: {
            handleEdit($event) {
                // 显示/隐藏编辑框
                this.isEdit = !this.isEdit;
                // 当情况是输入完毕转换成显示时
                if (this.isEdit !== true) {
                    // 确保输入的值不为空
                    if ($event.target.value.trim()) {
                        // 保存
                        this.changeTask(this.task, $event.target.value);
                    } else {
                        // 为空则提示
                        console.log('输入不能为空');
                        return
                    }
                // 当情况是显示状态转换成输入时
                } else {
                    // 在下一次DOM更新结束后执行回调
                    this.$nextTick(function() {
                        // 自动焦点输入框
                        this.$refs.inputContent.focus()
                    })
                }
            }
        }
    }
</script>

<style scoped>
    li:hover {
        background-color: #f0f0f0;
    }

    .task_item {
        overflow: hidden;
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

    .edit_content {
        float: left;
        margin-left: 15px;
        height: 22px;
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


    .task-enter-active {
        animation: anm 1s linear;
    }

    .task-leave-active {
        animation: anm 1s linear reverse;
    }

    @keyframes anm {
        from {
            transform: translateX(-100%);
        }
        to {
            transform: translateX(0px);
        }
    }
</style>
