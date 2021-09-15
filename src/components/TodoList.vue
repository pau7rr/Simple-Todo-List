<template lang="es">
<div class="task-list">
    <form class="form" @submit.prevent="createTasks">
        <label class="label" for="task">New task: </label>
        <input class="input" type="text" v-model="newTask" id="task"> 
        <input class="button" type="submit" value="Create task">
        <input class="button2" value="Clear All" @click.prevent="deleteTask">
    </form>
        <ul class="list">
            <li 
            class="task"
            v-for="(task, i) in tasks" 
            :key="'task' + i"
            :class="{completed: task.completed}"
            @click="completeTask(task.id)"
            >
            {{task.text}} 
            </li>     
        </ul>
    </div>
</template>
<script>
let counter = 0;
export default {
    data: () => ({
        newTask: "",
        tasks: [],
    }),
    methods: {
        createTasks(){
            if (!this.newTask) return

            let task = {
                id: counter++,
                text: this.newTask,
                completed: false,
            }
            this.tasks.push(task),
            this.newTask = ""
        },
        completeTask(id){
            let findTask = this.tasks.find( obj => {
                return obj.id === id
            })
            if (findTask.completed) return findTask.completed = false
                
            findTask.completed = true
        },
        deleteTask(){
            this.tasks = []
        }
    }
}
</script>
<style scoped>
    .task-list {
        width: 800px;
        max-width: 100%;
        margin: 0px auto;
    }
    .form {
        background: white;
        border-radius: 12px;
        padding: 30px;
        box-shadow: 0px 10px 22px -1px rgba(0,0,0,0.25);
        margin-top: 10px;
    }
    .label {
        display: block;
        margin-bottom: 10px;
    }
    .input {
        height: 35px;
    }
    .button {
        margin-left: 20px;
        height: 35px;
        border: none;
        border-radius: 5px;
        box-shadow: 0 1px 4px rgba(0, 0, 0, .2);
        background-color: darkred;
        color: #ecf0f1;
        cursor: pointer
    }
    .button2 {
        text-align: center;
        width: 70px;
        margin-left: 20px;
        height: 35px;
        border: none;
        border-radius: 5px;
        box-shadow: 0 1px 4px rgba(0, 0, 0, .2);
        background-color: darkred;
        color: #ecf0f1;
        cursor: pointer
    }
    .list {
        margin-top: 40px;
    }
    .task {
        cursor: pointer;
        margin: 10px 0;
    }
    .completed {
        color: darkred;
        text-decoration: line-through;
    }
    .trash {
        color: white;
        text-decoration: line-through;
        margin-left: 20px;
    }
</style>