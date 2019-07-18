<template>
    <v-layout row class="py-3 px-4">
        <v-flex sm12 xs12 md6 class='pa-2'>
            <v-card class="pa-2">
                <v-form>
                    <v-text-field
                            v-model="task"
                            label="Task.."
                            outline
                            type="text"
                    >

                    </v-text-field>
                    <v-textarea
                            v-model="description"
                            label="Enter Description.."
                            outline
                    >

                    </v-textarea>
                    <v-btn
                            v-if="edit!=true"
                            color="primary"
                            @click="addTask(task,description,$event)"
                            dark
                    >
                        Add Task
                    </v-btn>

                    <v-btn
                            v-if="edit==true"
                            color="success"
                            @click="updateTask($event)"
                            dark
                    >
                        Update
                    </v-btn>

                    <v-btn
                            v-if="edit==true"
                            color="secondary"
                            @click="cancelTask($event)"
                            dark
                    >
                        Cancel
                    </v-btn>
                </v-form>
            </v-card>
        </v-flex>

        <v-flex sm12 xs12 md6>
            <v-flex xs12
                    v-for="(task,index) in tasks"
                    :key="task.index"
                    >
                <v-card class="px-3 mb-2">
                    <v-card-title class="heading">
                        Task: {{task.task}}
                    </v-card-title>
                    <v-card-text>
                        Description: {{task.description}}
                    </v-card-text>
                    <v-card-actions v-if="edit == false">
                        <v-btn  color="primary"
                                @click="editTask(task,index)"
                                dark>
                            Edit
                        </v-btn>
                        <v-btn  color="error"
                                @click="deleteTask(index)"
                                dark>
                            Delete
                        </v-btn>
                    </v-card-actions>

                    <v-card-actions v-if="edit != false">
                        <v-btn  color="primary"
                                disabled
                                dark>
                            Edit
                        </v-btn>
                        <v-btn  color="error"
                                disabled
                                dark>
                            Delete
                        </v-btn>
                    </v-card-actions>
                </v-card>

            </v-flex>
        </v-flex>
    </v-layout>
</template>

<script>
    export default {
        name: "Task",
        data:()=>({
            task:'',
            description:'',
            edit:false,
            delete:false,
            cancel:false,
            id2:0,
            ind:0,
            tasks:[]
        }),
        methods:{
            addTask(t,d,e){
                e.preventDefault();
                this.tasks.push({
                    task:this.task,
                    description:this.description
                });
                localStorage.setItem('task',JSON.stringify(this.task));
                this.task = '';
                this.description = '';
            },
            editTask(t,i){
                this.edit =!this.edit;
                this.task =t.task;
                this.description = t.description;
                this.ind = i;
            },
            updateTask(e){
                e.preventDefault();
                this.edit =!this.edit;
                let taskdb = {
                    task: this.task,
                    description:this.description
                };
                this.tasks[this.ind] = taskdb;
                localStorage.setItem('tasks',JSON.stringify(this.tasks));
                let taskDB = JSON.parse(localStorage.getItem('tasks'));
                this.tasks = taskDB;
                this.task = '' ;
                this.description = '';
            },
            cancelTask(e){
                e.preventDefault();
                this.task = '' ;
                this.description = '';
                this.edit = !this.editTask;
            },
            deleteTask(i){
                this.tasks.splice(i,1);
                localStorage.setItem('tasks',JSON.stringify(this.tasks))
            }
        },
        created(){
              let taskDB =JSON.parse(localStorage.getItem('tasks'));
              if(taskDB == null) {
                  this.tasks = [];
              }
              else{
                  this.tasks = taskDB;
              }
        }
    }
</script>

<style scoped>

</style>