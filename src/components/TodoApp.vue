<template>
  <div class="wrapper">
    <header>
      <div><img alt="" class="logo" src="../assets/logo.png"/></div>
      <div>SHAPKIN</div>
      <div class="theme">
        <div>Темная тема</div>
        <RockerSwitch/>
      </div>
    </header>

    <main>
      <div class="container" style="max-width: 600px">
        <h2 class="text-center mt-5">Список дел</h2>

        <div class="d-flex mt-5">
          <input
              v-model="task"
              class="w-100 form-control"
              placeholder="Введите задачу"
              type="text"
          />
          <button class="btn btn-warning rounded-0 button" @click="submitTask">
            Создать
          </button>
        </div>

        <table class="table table-bordered mt-5">
          <thead>
          <tr>
            <th scope="col">Задача</th>
            <th scope="col" style="width: 120px">Статус</th>
            <th class="text-center" scope="col">Удалить</th>
            <th class="text-center" scope="col">Изменить</th>
          </tr>
          </thead>
          <tbody>
          <tr v-for="(task, index) in tasks" :key="index">
            <td>
            <span :class="{ 'line-through': task.status === 'finished' }">
              {{ task.name }}
            </span>
            </td>
            <td>
            <span
                :class="{
                'text-danger': task.status === 'to-do',
                'text-success': task.status === 'finished',
                'text-warning': task.status === 'in-progress',
              }"
                class="pointer noselect"
                @click="changeStatus(index)"
            >
              {{ capitalizeFirstChar(task.status) }}
            </span>
            </td>
            <td class="text-center">
              <div @click="deleteTask(index)">
                <span class="fa fa-trash pointer"></span>
              </div>
            </td>
            <td class="text-center">
              <div @click="editTask(index)">
                <p class="fa fa-pen pointer"></p>
              </div>
            </td>
          </tr>
          </tbody>
        </table>
      </div>
    </main>

    <footer>
      <div>191-362</div>
      <div>Шапкин Давид Димитров</div>
      <div>09.07.2021</div>
    </footer>


  </div>
</template>

<script>
// Import package
import RockerSwitch from "vue-rocker-switch";
// Import styles
import "vue-rocker-switch/dist/vue-rocker-switch.css";


export default {
  name: "App",
  components: {
    RockerSwitch
  },
  props: {
    msg: String,
  },


  data() {
    return {
      darkTheme: false,
      theme: 0,
      task: "",
      editedTask: null,
      statuses: ["Надо сделать", "В процессе", "Готово"],

      /* Status could be: 'to-do' / 'in-progress' / 'finished' */
      tasks: [
        {
          name: "Пойти в магазин",
          status: "Надо сделать",
        },
        {
          name: "Помыть посуду",
          status: "В процессе",
        },
        {
          name: "Сделать экзамен на VUE",
          status: "Готово",
        },
      ],
    };
  },

  methods: {

    capitalizeFirstChar(str) {
      return str.charAt(0).toUpperCase() + str.slice(1);
    },


    changeStatus(index) {
      let newIndex = this.statuses.indexOf(this.tasks[index].status);
      if (++newIndex > 2) newIndex = 0;
      this.tasks[index].status = this.statuses[newIndex];
    },


    deleteTask(index) {
      this.tasks.splice(index, 1);
    },


    editTask(index) {
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },

    submitTask() {
      if (this.task.length === 0) return;

      if (this.editedTask != null) {
        this.tasks[this.editedTask].name = this.task;
        this.editedTask = null;
      } else {

        this.tasks.push({
          name: this.task,
          status: "Надо сделать",
        });
      }

      this.task = "";
    },
  },
};


</script>

<style scoped>
.button {
  background-color: rgba(252, 39, 148, 0.57);
}

.button:hover {
  background-color: rgba(129, 2, 66, 0.57);
}

header {
  font-weight: bold;
  background-color: rgba(246, 150, 197, 0.57);
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.wrapper {
  background-color: rgba(246, 150, 197, 0.57);
}

main {
}

footer {
  margin-top: 50px;
  font-weight: bold;
  background-color: rgba(246, 150, 197, 0.57);
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.wrapper {
  margin-right: 10%;
  margin-left: 10%;

}

.logo {
  width: 30%;
}


.pointer {
  cursor: pointer;
}

.noselect {
  -webkit-touch-callout: none; /* iOS Safari */
  -webkit-user-select: none; /* Safari */
  -khtml-user-select: none; /* Konqueror HTML */
  -moz-user-select: none; /* Old versions of Firefox */
  -ms-user-select: none; /* Internet Explorer/Edge */
  user-select: none;
  /* Non-prefixed version, currently
                                   supported by Chrome, Edge, Opera and Firefox */
}

.line-through {
  text-decoration: line-through;
}
</style>
