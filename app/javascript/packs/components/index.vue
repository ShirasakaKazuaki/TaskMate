<template>
<div class="container">
<!-- 入力フォーム  -->
	<div style="text-align: right;">
        <input v-model="newTask" class="form-control my-3 p-4" placeholder="タスクを書こう">
		<div v-on:click="createTask" class="btn btn-success px-4 mb-5">
			タスク追加
		</div>
	</div>
    <pre>{{ $data }}</pre>
	
<!-- タスクリスト  -->
	<div>
		<ul class="list-group">
            <li v-if="task.is_done == false" v-for="task in tasks" v-bind:id="'row_task_' + task.id" class="list-group-item align-items-center">
                <input type="checkbox" v-on:change="doneTask(task.id)" v-bind:id="'task_' + task.id" />
                <label v-bind:for="'task_' + task.id">{{ task.name }}</label>
            </li>
        </ul>
	</div>
	
	<!-- 表示ボタン -->
    <div class="btn btn-info mt-4 mb-2" v-on:click="displayFinishedTasks">完了済みタスクを表示</div>
	
	<!-- 完了済みタスク一覧 -->
    <div id="finished-tasks" class="display_none">
        <ul class="list-group">
            <li v-for="task in tasks" v-if="task.is_done" v-bind:id="'row_task_' + task.id" class="list-group-item align-items-center">
                <input type="checkbox" v-bind:id="'task_' + task.id" checked="checked">
                <label v-bind:for="'task_' + task.id"  class="line-through">{{ task.name }}</label>
            </li>
        </ul>
    </div>

</div>
</template>

<script>
    import axios from 'axios';
    export default {
        data: function () {
            return {
                tasks: [],
                newTask: ''
            }
        },
        mounted: function () {
            this.addTasks();
        },
        methods: {
            addTasks: function () {
                axios.get('/api/tasks').then((response) => {
                    for(var i = 0; i < response.data.tasks.length; i++) {
                        this.tasks.push(response.data.tasks[i]);
                    }
                }, (error) => {
                    console.log(error);
                }); 
            },
            displayFinishedTasks: function() {
                document.querySelector('#finished-tasks').classList.toggle('display_none');
            },
            createTask: function () {
                if(this.newTask == '') return;
                axios.post('/api/tasks', { task: { name: this.newTask } }).then((response) => {
                    console.log(response);
                    this.tasks.unshift(response.data);
                    this.newTask = '';
                }, (error) => {
                    console.log(error);
                });        
            },
            doneTask: function (task_id) {
                axios.put('/api/tasks/' + task_id, { task: { is_done: true } }).then((response) => {
                    this.moveFinishedTask(task_id);
                    this.tasks[response.data.id -1 ].is_done = true;
                }, (error) => {
                    console.log(error);
                });
            }, 
            moveFinishedTask: function(task_id) {
                var el = document.querySelector('#row_task_' + task_id);
                var el_clone = el.cloneNode(true);
                el.classList.add('display_none');
                el_clone.getElementsByTagName('input')[0].checked = 'checked';
                el_clone.getElementsByTagName('label')[0].classList.add('line-through');
                var li = document.querySelector('#finished-tasks > ul > li:first-child');
                document.querySelector('#finished-tasks > ul').insertBefore(el_clone, li);
            }
        }
    }
</script>

<style scoped>
    [v-cloak] {
        display: none;
    }
    .display_none {
        display:none;
    }
    .line-through {
        text-decoration: line-through;
    }
</style>