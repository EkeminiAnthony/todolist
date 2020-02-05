<template>
    <div>
         <div class="container mt-4">
            <h1 style="color: pink"><img src="bee.png" alt="" width="50px">Kemzy Pixels TODO List</h1>
            <hr>
        </div>

        <div class="container">          
            <div class="row">
               
        <div class="col-md-4">
            <div class="card shadow p-4">
                <h2 class="mb-4">TODO</h2>

                <form @submit.prevent = "addUser">
                    <div class="form-group">
                        <label>Reminder/Task</label>
                        <input v-model="user.task" type="text"  class="form-control">    
                    </div>

                    <div class="form-group">
                        <label>Date</label>
                        <input v-model="user.date" type="text"  class="form-control">    
                    </div>

                    <div class="form-group">
                        <label>Time</label>
                        <input v-model="user.time" type="text"  class="form-control">    
                    </div>

                    <!-- <div class="form-group">
                        <label>Frequency</label>
                        <input v-model="user.frequency" type="text"  class="form-control">    
                    </div> -->

                    <div class="form-group">
                      <label>Frequency</label>
                      <select class="form-control" v-model="user.frequency">
                      <option disable selected class="active">Choose an option</option>
                      <option value="daily">Daily</option>
                      <option value="weekly">Weekly</option>
                      <option value="monthly">Monthly</option> 

                      </select>

                    </div>

                     <div class="form-group">
                      <label>status</label>
                      <select class="form-control" v-model="user.status">
                      <option disable selected class="active">Choose an option</option>  
                      <option value="todo">Todo</option>
                      <option value="doing">Doing</option>
                      <option value="done">Done</option> 

                      </select>

                    </div>
                    
                    <div class="form-group">
                        <button v-if="status" type="submit" class="btn btn-dark">Add New Task</button>                                             
                        <button v-if="secondStatus"  type="click" @click.prevent="updateTodo" class="btn btn-info ml-5">Update</button>
                        <button type="reset" class="btn btn-danger ml-3" @click="back">Reset</button>                                           
                    </div> 

                </form>
        </div>
    </div>
     <div  class="col-md-8">
                    <table class="table border">
                        <thead>
                          <tr>
                            <th scope="col">S/N</th>  
                            <th scope="col">Reminder/Task</th>
                            <th scope="col">Date</th>
                            <th scope="col">Time</th>
                            <th scope="col">Frequency</th>
                            <th scope="col">Status</th>
                            <th>Actions</th>
                            
                          </tr>
                        </thead>
                        <tbody>
                          <tr v-for="(todo,index) in todo" :key="index">  
                            <th scope="row">{{parseInt(index) + 1}}</th>
                            <td>{{todo.task}}</td>
                            <td>{{todo.date}}</td>
                            <td>{{todo.time}}</td>
                            <td>{{todo.frequency}}</td>
                            <td>{{todo.status}}</td>
                            <td>
                                <button class="btn btn-dark" @click="removeItem(index)">Delete</button>
                                <button class="btn btn-secondary ml-3" @click="updateItem(todo)">Edit</button>
                               
                            </td>                            
                          </tr>                                                    
                        </tbody>
                      </table>
        </div>

    </div>
</div>

        <div class="container mt-4">
          <h6 style="text-align: center">&copy;TODO List  @Project Create</h6>
            <hr>
        </div>

    </div>
</template>


<script>
import swal from 'sweetalert';
export default {
    data(){
        return{
      status: true,
      secondStatus: false,
      message: "Hello Vue",
      todo: [
            {task: "host project", date: "05-02-2020", time:"2:00pm", frequency: "daily", status:"todo"},
            {task: "Commit to Git", date: "06-02-2020", time:"1:00pm", frequency: "weekly", status:"doing"},
            {task: "Travel out of the country", date: "07-02-2020", time:"6:00am", frequency: "monthly", status:"done"},
            
       ],
        
        user : 
          {
              task : "",
              date : "",
              time : "",
              frequency : "",
              status : "",
        },
        myTodoToUpdate: null,
        editArea: null,
        
      }
    },

    methods: {
      addUser(){
        this.todo.push(this.user)
        swal("waoh!", "your todo is added!", "success");       
      },
      removeItem(index) {        
       
      swal({
            title: "Are you sure?",
            text: "Once deleted, task will be lost!",
            icon: "warning",
            buttons: true,
            dangerMode: true,
            })
            .then((willDelete) => {
            if (willDelete) {
              this.todo.splice(index, 1); 
            swal("Todo successfully deleted!", {
              icon: "success",
            });
            } else {
            swal("Your Todo is safe!");
            }
      });

        // alert("Delete me");
      },
      updateItem(id){
        // console.log(id);
        // this.user.name = id.name;
        // this.user.role = id.role;

        this.status = false;
        this.secondStatus = true;
        this.user = id;
        this.myTodoToUpdate = this.todo.indexOf(id)
        this.todo[this.myTodoToUpdate] = this.user
      },
      updateTodo(){
        this.secondStatus = false;
        this.status = true;
        // this.user = ''
      },
      // updateTodo() {
      //    alert('hello');
      // },
      back(){
        this.status = true;
        this.secondStatus = false;
      }
    }
    
    
    }


</script>



<style scoped>
    


</style>