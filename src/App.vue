<template>
  <form action="">
    <div id="app">
      <div id="header">
        <h2>T O D O</h2>
        <div id="inputField">
          <input
            v-model="taskName"
            class="form-control"
            type="text"
            placeholder="Enter the task"
            id="taskEnterText"
            autocomplete="off"
          />
          <button
            @click="addTask"
            type="button"
            style="margin-left: 10px"
            class="btn btn-primary btn-xl"
          >
            <i class="fa fa-plus">&nbsp;<b>ADD</b></i>
          </button>
        </div>
      </div>
      <div id="list">
        <table class="table table-striped">
          <thead>
            <tr>
              <th scope="col" style="width: 70%">Task</th>
              <th scope="col" style="width: 20%; text-align: center">Status</th>
              <th
                scope="col"
                style="width: 10%; text-align: center"
                colspan="2"
              >
                Action
              </th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(task, index) in tasks" :key="index">
              <td>
                <span :class="{ isDone: task.status === 'Completed' }">{{
                  task.task
                }}</span>
              </td>
              <td style="text-align: center">
                <label>{{ task.status }}</label>
              </td>
              <td style="text-align: left">
                <button
                  type="button"
                  class="btn btn-success btn-sm"
                  @click="completeTask(index)"
                >
                  <i class="fa fa-check"></i>
                </button>
              </td>
              <td style="text-align: right">
                <button
                  type="button"
                  class="btn btn-outline-danger btn-sm"
                  @click="removeTask(index)"
                >
                  <i class="fa fa-trash"></i>
                </button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </form>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      tasks: [],
    };
  },
  methods: {
    addTask() {
      if (this.taskName.length !== 0) {
        console.log(this.taskName.length);
        this.tasks.push({
          task: this.taskName,
          status: "To-Do",
        });
        this.taskName = "";
      }
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
    },
    completeTask(index) {
      var status = this.tasks[index].status;
      if (status === "To-Do") {
        this.tasks[index].status = "Completed";
      } else {
        this.tasks[index].status = "To-Do";
      }
    },
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

h2 {
  padding: 1% 0 0 20%;
  color: white;
}

#header {
  background-image: url("assets/header_bg.jpg");
  background-repeat: no-repeat;
  height: 120px;
  background-size: cover;
  position: relative;
}

#inputField {
  display: flex;
  width: 60%;
  margin: auto;
}

#list {
  width: 60%;
  margin: 20px auto;
}

.btn {
  cursor: pointer;
}

.isDone {
  text-decoration: line-through;
}
</style>
