<template>
    <div class="container">
        <div class="text-center mt-5">
            My Todo App
        </div>
    </div>
    
    <!--Input -->
    <div class="d-flex">
        <input v-model = "task" type="text" placeholder = "Enter Text" class="form-control">
        <button @click="submitTask" class = "btn btn-warning rounded-0">SUBMIT</button>
    </div>

    <!--Task Table -->
    <table class="table table-bordered mt-5">
        <thead>
            <tr>
            <th scope="col">Task</th>
            <th scope="col">Status</th>
            <th scope="col" class = "text-center">#</th>
            <th scope="col" class = "text-center">#</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for = "(task, index) in tasks" :key = "index">
                <td>{{task.name}}</td>
                <td style = "width: 120px"><span @click = "changeStatus(index)" class = "pointer">{{task.status}}</span></td>
                <td>
                    <div class = "text-center" @click = "editTask(index)">
                        <span class = "fa fa-pen" ></span>
                    </div>
                </td>
                <td>
                    <div class = "text-center" @click="deleteTask(index)">
                        <span class = "fa fa-trash"></span>
                    </div>
                </td>
            </tr>
        </tbody>
    </table>
</template>

<script>
    export default{
        name: "Todo App",
        props: {
            msg: String
        },
        data(){
            return{
                task : "",
                editedTask: null,
                availableStatuses: ["to-do", "in-progress", "finished"],
                tasks: [
                    {
                        name: "Understand the component structure of a Vue App",
                        status: "in-progress"
                    },
                    {
                        name: "Build a todo App with Vue",
                        status: "in-progress"
                    },
                ]
            }
        },
        methods : {
            submitTask(){
                if(this.task.length === 0) return

                if(this.editedTask == null){
                    this.tasks.push({
                        name: this.task,
                        status: "to-do"
                    })
                }else{
                    this.tasks[this.editedTask].name = this.task;
                    this.editedTask = null
                }
                

                this.task = ""
            },

            deleteTask(index){
                this.tasks.splice(index, 1)
            },

            editTask(index){
                this.task = this.tasks[index].name;
                this.editedTask = index
            },
            changeStatus(index){
                let newIndex = this.availableStatuses.indexOf(this.tasks[index].status);
                if(++newIndex > 2) newIndex = 0;
                this.tasks[index].status = this.availableStatuses[newIndex]
            }

        }
    }
</script>

<style class = "scoped">
    .pointer {
        cursor: pointer
    }
</style>

