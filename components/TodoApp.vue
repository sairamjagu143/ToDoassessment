<template>
  <div class="container" style="max-width: 600px">
    <!-- Heading -->
    <h2 class="text-center mt-5">Sample To Do List Application</h2>

    <!-- Input -->
    <div class="p-5" >
        <div class="row p-2">
      <input
        type="text"
        v-model="task"
        placeholder="Enter task"
        class="w-100 form-control"
      />
        </div>
    <!--Summary-->
     <div class="row p-2">
       <input
        type="text"
        v-model="summary"
        placeholder="Enter summary"
        class="w-100 form-control"
      />
     </div>
      <!--Discription-->
       <div class="row p-2">
      <textarea v-model="discription"
        placeholder="Enter Discription"
        class="w-100 form-control">
      </textarea>
       </div>
        <!--Date-->
       <div class="row p-2">
       <input
        type="date"
        v-model="date"
        class="w-100 form-control"
      />
     </div>
      <button class="btn btn-success rounded-0" @click="submitTask">
        SUBMIT
      </button>
    </div>
  </div>
   
    <!-- Task table -->
    <div class="container">
    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <th scope="col">Task</th>
          <th scope="col" style="width: 120px">summary</th>
          <th scope="col">Desciption</th>
          <th scope="col">Due Date</th>
          <th scope="col" class="text-center">#</th>
          <th scope="col" class="text-center">#</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <td>
            
              {{ task.name }}
    
          </td>
          
          <td>
            <span>
                {{task.summ}}
            </span>
          </td>
          <td>
            <span>
                {{task.desc}}
            </span>
          </td>
           <td>
            <span>
                {{task.dt}}
            </span>
          </td>
          <td class="text-center">
            <div @click="deleteTask(index)">
              <span class="text-danger pointer">delete</span>
            </div>
          </td>
          <td class="text-center">
            <div @click="editTask(index)">
              <p class="text-warning pointer">Edit</p>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      task: "",
      summary:"",
      discription:"",
      date:"",
      editedTask: null,
      tasks: [],
    };
  },
  methods: {
    
    
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    
    editTask(index) {
      this.task = this.tasks[index].name;
      this.summary = this.tasks[index].summ;
      this.discription = this.tasks[index].desc;
      this.date = this.tasks[index].dt;
      this.editedTask = index;
    },
   
    submitTask() {
      if (this.task.length === 0) return;
      /* We need to update the task */
      if (this.editedTask != null) {
        this.tasks[this.editedTask].name = this.task;
        this.tasks[this.editedTask].summ = this.summary;
        this.tasks[this.editedTask].desc = this.discription;
        this.tasks[this.editedTask].dt = this.date;
        this.editedTask = null;
      } else {
        /* We need to add new task */
        this.tasks.push({
          name: this.task,
          summ: this.summary,
          desc: this.discription,
          dt:this.date,
        });
      }
      this.task = "";
      this.summary="";
      this.discription="";
      this.date="";
    },
  },
};

</script>

<style scoped>
.pointer {
  cursor: pointer;
}
.noselect {
  -webkit-touch-callout: none; /* iOS Safari */
  -webkit-user-select: none; /* Safari */
  -khtml-user-select: none; /* Konqueror HTML */
  -moz-user-select: none; /* Old versions of Firefox */
  -ms-user-select: none; /* Internet Explorer/Edge */
  user-select: none; /* Non-prefixed version, currently supported by Chrome, Edge, Opera and Firefox */
}

</style>