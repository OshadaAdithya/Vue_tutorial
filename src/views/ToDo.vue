<template>
    <div class="set1">
        
        <img alt="todo" class="todo" src="../assets/todo.png" width="100" height="100" />
        <h1>Task List</h1>
    </div>
    <div class="centered-container">
        <div class="d-flex align-items-center justify-content-center">
            <input type="text" placeholder="Type something" class="form-control" v-model="task_item">
            <button @click="submitTask" class="btn btn-primary">Submit</button>
            <button @click="deleteAll" class="btn btn-danger">Clear</button>
        </div>
        <div class="check" v-if="showWarning">
            <p>Please enter something</p>
        
        </div>
        
        <div class="list">
        <table class="table table-bordered mt-4">
            <thead>
                <tr>
                <th scope="col">id</th>
                <th scope="col">Task</th>
                <th scope="col" style="width: 180px;">Status</th>
                <th scope="col" style="width: 80px;" class="text-center">#</th>
                <th scope="col" style="width: 80px;" class="text-center">#</th>
                </tr>
            </thead>
            <tbody>
            <tr v-for="todo in tasks" :key="todo.id">
                <td>{{ todo.id }}</td>
            <td>
                <template v-if="!todo.editing">{{ todo.name }}</template>
                <input type="text" v-else v-model="todo.name" @keyup.enter="saveTask(todo)">
                
            </td>
            <td>
                <select v-model="todo.status">
                    <option value="A">In-Progress</option>
                    <option value="B">Done</option>
                    <option value="C">To-Do</option>
                </select>
                
            </td>
            <td>
                <div class="text-center" @click="editTask(todo)">
                <span class="fa fa-edit"></span>
                </div>
            </td>
            <td>
                <div class="text-center" @click="deleteTask(todo)">
                <span class="fa fa-trash-alt"></span>
                </div>
            </td>   
            </tr>
    
            </tbody>
        </table>
        
        </div>
    </div>

</template>

<script>
export default {
    data(){
        return{
            tasks:[]
               /*{id: 1,name: 'first task',  status: 'in progress', editing:false},
               {id: 2,name: 'second task',  status: 'in progress', editing:false}*/
            ,
            task_item:'',
            showWarning:false,
            statusTypes: ['In-progress', 'Completed', 'To-do']
        }
    },
    methods:{
        submitTask(){
           // this.tasks.
           if (this.task_item.trim() === '') {
            // If the task_item is empty or contains only spaces
            this.showWarning = true; // Show the warning message
            }
            else{
                
                this.tasks.push({
                    id: this.tasks.length + 1,
                    name:this.task_item,
                    status:'To-Do',
                    editing:false
                })
                this.task_item=''
                this.showWarning=false
            }

        },
        editTask(todo){
            const taskId= this.tasks.indexOf(todo)
            this.tasks[taskId].editing=true  //set editing condition true
            //this.tasks[id].editing=true  
        },
        saveTask(todo){
            const taskId = this.tasks.indexOf(todo);
            if (taskId==-1 && todo.name.trim() !== '') {
                this.tasks[taskId].editing = false;
            }

           
        },
        deleteTask(todo){
           
             console.log(todo);
             this.tasks.splice(this.tasks.indexOf(todo), 1);
        },

        deleteAll(){
            this.tasks=[];
        }
        }
    }


</script>

<style scoped>
.set1{
    text-align: center;
    margin: 0 auto;
    font-style: italic; 
    font-family: "Lucida Console", "Courier New", monospace;
    padding-bottom: 15px;
}
.centered-container{
    width: 80%; /* Adjust the width as needed */
    max-width: 800px;
    margin: 0 auto;
}

.check{
    
}
</style>