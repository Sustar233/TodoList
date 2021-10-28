<template>
    <div class="now">{{now}}</div>
</template>

<script>
  export default {
    name: 'NowT',
    computed: {
        // 获取当前日期
        now: function() {
            let date = new Date();
            let now = date.getMonth() + 1 + '月' + date.getDate() + '日  ' + date.getHours() + '时' + date.getMinutes() + '分'
            return now
        }
    }
  }
</script>


<style scoped>
    .now {
        float: left;
        margin-left: 60px;
        width: 150px;
        height: 40px;
        line-height: 40px;
        text-align: center;
        color: #4b4d52;
        background-color: #f7f7f7;
        border: 1px solid white;
        border-radius: 5px;
    }
</style>
