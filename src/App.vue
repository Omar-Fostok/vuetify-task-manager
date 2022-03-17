<template>
  <div id="app">
    <div class="circle-small"></div>
    <div class="circle-medium"></div>
    <div class="circle-big"></div>
    <div class="tri-holder">
      <div class="triangle"></div>
    </div>
    <!-- new dialog -->
    <template>
      <div class="text-center">
        <v-dialog v-model="dialog2" width="500">
          <template v-slot:activator="{ on, attrs }">
            <div v-bind="attrs" v-on="on"></div>
          </template>

          <v-card style="overflow: hidden">
            <v-card-title class="text-h6 lighten-2">
              <font-awesome-icon
                icon="fa-solid fa-table"
                style="color: #00a3ff"
              />&nbsp;&nbsp;
              <span style="color: #0a223d"> Design Team Board </span>
              <div class="close-x" @click="dialog2 = false">
                <font-awesome-icon icon="fa-solid fa-x" />
              </div>
            </v-card-title>
            <v-row style="margin-left: 2vh">
              <v-col class="d-flex" cols="4" sm="4">
                <v-select :items="columns" v-model="colName2" solo></v-select>
              </v-col>
              <v-col class="d-flex" cols="4" sm="4">
                <v-select
                  :items="priority"
                  v-model="val2"
                  solo
                  :background-color="backColor3"
                ></v-select>
              </v-col>
            </v-row>

            <v-card-text style="position: relative">
              <div
                style="
                  position: absolute;
                  left: 0px;
                  font-size: 3.5vh;
                  font-weight: bold;
                  color: #0a223d;
                  top: 0;
                  left: 4vh;
                  line-height: 7vh;
                "
              >
                Task:
              </div>
              <v-text-field
                label="Task..."
                solo
                style="width: 83%; margin-left: 17%; display: inline-block"
                v-model="taskName2"
              >
              </v-text-field>
            </v-card-text>
            <h3 style="color: #0a223d; margin-left: 4vh">Description</h3>
            <v-textarea
              solo
              name="input-7-4"
              label="Description..."
              rows="3"
              style="width: 90%; margin-left: 4vh"
              v-model="description2"
            ></v-textarea>
            <h3 style="color: #0a223d; margin-left: 4vh">Comments</h3>
            <v-textarea
              solo
              name="input-7-4"
              label="Comments..."
              rows="3"
              style="width: 90%; margin-left: 4vh"
              v-model="comments2"
            ></v-textarea>
            <v-divider></v-divider>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="red" text @click="deleteTask()"> delete </v-btn>
              <v-btn color="primary" text @click="editElement()"> Save </v-btn>
              <v-spacer></v-spacer>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </div>
    </template>
    <!-- end new dialog -->
    <!-- Start of dialog -->

    <template>
      <div class="text-center">
        <v-dialog v-model="dialog" width="500">
          <template v-slot:activator="{ on, attrs }">
            <div v-bind="attrs" v-on="on"></div>
          </template>

          <v-card style="overflow: hidden">
            <v-card-title class="text-h6 lighten-2">
              <font-awesome-icon
                icon="fa-solid fa-table"
                style="color: #00a3ff"
              />&nbsp;&nbsp;
              <span style="color: #0a223d"> Design Team Board </span>
              <div class="close-x" @click="dialog = false">
                <font-awesome-icon icon="fa-solid fa-x" />
              </div>
            </v-card-title>
            <v-row style="margin-left: 2vh">
              <v-col class="d-flex" cols="4" sm="4">
                <v-select :items="columns" solo v-model="colName"></v-select>
              </v-col>
              <v-col class="d-flex" cols="4" sm="4">
                <v-select
                  :items="priority"
                  v-model="val"
                  solo
                  :background-color="backColor2"
                ></v-select>
              </v-col>
            </v-row>

            <v-card-text style="position: relative">
              <div
                style="
                  position: absolute;
                  left: 0px;
                  font-size: 3.5vh;
                  font-weight: bold;
                  color: #0a223d;
                  top: 0;
                  left: 4vh;
                  line-height: 7vh;
                "
              >
                Task:
              </div>
              <v-text-field
                label="Task..."
                solo
                style="width: 83%; margin-left: 17%; display: inline-block"
                v-model="taskName"
              >
              </v-text-field>
            </v-card-text>
            <h3 style="color: #0a223d; margin-left: 4vh">Description</h3>
            <v-textarea
              solo
              name="input-7-4"
              label="Description..."
              rows="3"
              style="width: 90%; margin-left: 4vh"
              v-model="description"
            ></v-textarea>
            <h3 style="color: #0a223d; margin-left: 4vh">Comments</h3>
            <v-textarea
              solo
              name="input-7-4"
              label="Comments..."
              rows="3"
              style="width: 90%; margin-left: 4vh"
              v-model="comments"
            ></v-textarea>
            <v-divider></v-divider>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="primary" text @click="addElement()"> Save </v-btn>
              <v-spacer></v-spacer>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </div>
    </template>

    <!-- End of dialog -->
    <v-app id="inspire">
      <v-content class="outer-body">
        <v-container>
          <v-row class="main-card">
            <div class="test">
              <div
                class="square"
                style="
                  border: 2px solid #00a3ff;
                  color: #00a3ff;
                  width: 7vh;
                  height: 7vh;
                  text-align: center;
                  line-height: 7vh;
                  display: inline-block;
                  border-radius: 2vh;
                  margin-right: 1.6vh;
                "
              >
                <font-awesome-icon icon="fa-solid fa-house" />
              </div>
              <div
                class="square"
                style="
                  border: 2px solid #00a3ff;
                  color: #00a3ff;
                  width: 7vh;
                  height: 7vh;
                  text-align: center;
                  line-height: 7vh;
                  display: inline-block;
                  border-radius: 2vh;
                  margin-right: 1.6vh;
                "
              >
                <font-awesome-icon icon="fa-solid fa-table" />
              </div>
              <div
                class="search"
                style="
                  background-color: #f0f4f9;
                  color: #a4b3c1;
                  line-height: 7vh;
                  width: 37vh;
                  margin-bottom: -2.4vh;
                  margin-left: 3vh;
                  height: 7vh;
                  display: inline-block;
                  border-radius: 2.5vh;
                  position: relative;
                "
              >
                <div
                  class="mag"
                  style="position: absolute; font-size: 3vh; left: 7%"
                >
                  <font-awesome-icon icon="fa-solid fa-magnifying-glass" />
                </div>
              </div>
              <div class="right" style="float: right; overflow: hidden">
                <table>
                  <tr>
                    <td>
                      <div
                        class="square"
                        style="
                          border: 2px solid #00a3ff;
                          background-color: #00a3ff;
                          color: white;
                          width: 7vh;
                          height: 7vh;
                          font-size: 3vh;
                          text-align: center;
                          line-height: 6.5vh;
                          display: inline-block;
                          border-radius: 2vh;
                          margin-right: 5vh;
                        "
                      >
                        +
                      </div>
                    </td>
                    <td>
                      <div
                        class="bell"
                        style="
                          border: 2px solid #00a3ff;
                          color: #00a3ff;
                          width: 7vh;
                          height: 7vh;
                          text-align: center;
                          line-height: 7vh;
                          display: inline-block;
                          border-radius: 2vh;
                          margin-right: 1.6vh;
                        "
                      >
                        <font-awesome-icon icon="fa-solid fa-bell" />
                      </div>
                    </td>
                    <td>
                      <div
                        class="square"
                        style="
                          border: 2px solid #00a3ff;
                          color: #00a3ff;
                          width: 7vh;
                          height: 7vh;
                          text-align: center;
                          line-height: 7vh;
                          display: inline-block;
                          border-radius: 2vh;
                          margin-right: 1.6vh;
                        "
                      >
                        <font-awesome-icon icon="fa-solid fa-circle-question" />
                      </div>
                    </td>
                    <td>
                      <div
                        class="square"
                        style="
                          border: 2px solid #00a3ff;
                          color: #00a3ff;
                          width: 7vh;
                          height: 7vh;
                          text-align: center;
                          line-height: 7vh;
                          display: inline-block;
                          border-radius: 2vh;
                          margin-right: 1.6vh;
                        "
                      >
                        <font-awesome-icon icon="fa-solid fa-gear" />
                      </div>
                    </td>
                    <td>
                      <img
                        src="@/assets/791224_man_512x512.png"
                        style="
                          width: 7vh;
                          height: 7vh;
                          border-radius: 50%;
                          outline: 2px solid white;
                          position: relative;
                          bottom: -0.5vh;
                          margin-left: 3.5vh;
                          z-index: 3;
                        "
                        alt=""
                      />
                    </td>
                  </tr>
                </table>
              </div>
              <div class="clear"></div>
            </div>

            <div class="test2" style="color: #0a223d">
              <v-divider style="margin-left: -10px; width: 120%"></v-divider>
              Design Team Board
              <div class="right" style="float: right; overflow: hidden">
                <table>
                  <tr>
                    <td>
                      <div
                        class="semi-img"
                        style="
                          background-color: white;
                          text-align: center;
                          color: #00a3ff;
                          line-height: 6.2vh;
                          font-weight: normal !important;
                          font-size: 3vh;
                          width: 6vh;
                          height: 6vh;
                          border-radius: 50%;
                          display: inline-block;
                          position: relative;
                          outline: 2px dashed #00a3ff;

                          z-index: 2;
                          right: -83px;
                          top: -8px;
                        "
                      >
                        +
                      </div>
                    </td>
                    <td>
                      <div
                        class="some-text"
                        style="
                          font-size: 2.5vh;
                          color: #0a223d;
                          position: relative;
                          right: -100px;
                          top: -6px;
                        "
                      >
                        Add a member
                      </div>
                    </td>
                    <td>
                      <div
                        class="avatar-imgs"
                        style="
                          position: relative;
                          right: -120px;
                          margin-top: 10px;
                        "
                      >
                        <img
                          src="@/assets/download.png"
                          alt=""
                          style="
                            width: 6vh;
                            height: 6vh;
                            border-radius: 50%;
                            outline: 2px solid white;
                            position: relative;
                            z-index: 1;
                          "
                        />
                        <div
                          class="semi-img"
                          style="
                            background-color: pink;
                            text-align: center;
                            color: #fe6781;
                            line-height: 6vh;
                            font-size: 2.5vh;
                            top: -2.2vh;
                            width: 6vh;
                            height: 6vh;
                            border-radius: 50%;
                            display: inline-block;
                            position: relative;
                            outline: 2px solid white;

                            z-index: 2;
                            left: -2.5vh;
                          "
                        >
                          RD
                        </div>
                        <img
                          src="@/assets/791224_man_512x512.png"
                          style="
                            width: 6vh;
                            height: 6vh;
                            border-radius: 50%;
                            outline: 2px solid white;
                            position: relative;
                            left: -5.5vh;
                            z-index: 3;
                          "
                          alt=""
                        />
                        <div
                          class="semi-img"
                          style="
                            background-color: #7ddaf4;
                            text-align: center;
                            color: rgb(18 144 179);
                            line-height: 6vh;
                            font-size: 2.5vh;
                            top: -2.2vh;
                            width: 6vh;
                            height: 6vh;
                            border-radius: 50%;
                            display: inline-block;
                            position: relative;
                            outline: 2px solid white;

                            z-index: 4;
                            left: -8vh;
                          "
                        >
                          +16
                        </div>
                      </div>
                    </td>
                    <td>
                      <div
                        class="virtual-selector"
                        style="
                          width: 50%;
                          position: relative;
                          right: -97px;
                          top: 10px;
                        "
                      >
                        <v-select
                          label="All Tasks"
                          solo
                          dark
                          style="font-weight: normal !important"
                          background-color="#00a3ff"
                          readonly
                        ></v-select>
                      </div>
                    </td>
                  </tr>
                </table>
              </div>
              <div class="clear"></div>
            </div>
            <v-layout class="columns-4" align-start justify-center>
              <v-flex xs4 class="pa-3 ma-2">
                <v-list two-line class="each-col">
                  <v-subheader class="subheader">
                    Backlog
                    <div class="counter">{{ tasks.length }}</div>
                    <!-- Start of dialog -->

                    <div
                      @click="
                        taskName = '';
                        description = '';
                        comments = '';
                        val = 'Low';
                        dialog = true;
                        colName = columns[0].value;
                      "
                      class="add-button"
                    >
                      +
                    </div>
                  </v-subheader>

                  <draggable
                    v-model="tasks"
                    :options="{ group: 'people' }"
                    class="draggables"
                  >
                    <template v-for="task in tasks">
                      <v-list-tile
                        :key="task.id"
                        class="task"
                        @click="
                          passValuesToDialog(task);
                          colName2 = columns[0].value;
                          preCol = columns[0].value;
                        "
                      >
                        <v-list-tile-content>
                          <div v-html="task.taskName"></div>
                          <div class="priority-container">
                            <div class="messages">
                              <font-awesome-icon
                                icon="fa-regular fa-message"
                                style="color: grey"
                              />
                              <div class="n-messages">
                                {{ task.nMessages }}
                              </div>
                            </div>
                            <div class="attach">
                              <font-awesome-icon
                                icon="fa-solid fa-link"
                                style="color: grey"
                              />
                              <div class="n-attach">
                                {{ task.nAttach }}
                              </div>
                            </div>
                            <div
                              class="priorityName"
                              :style="{
                                background: task.backClr,
                                color: task.txtClr,
                              }"
                              v-html="task.priorityName"
                            ></div>
                          </div>
                        </v-list-tile-content>
                      </v-list-tile>
                    </template>
                  </draggable>
                </v-list>
              </v-flex>
              <v-flex xs4 class="pa-3 ma-2">
                <v-list two-line class="each-col">
                  <v-subheader class="subheader">
                    In Progress
                    <div class="counter">{{ tasks2.length }}</div>

                    <div
                      @click="
                        taskName = '';
                        description = '';
                        comments = '';
                        val = 'Low';
                        dialog = true;
                        colName = columns[1].value;
                      "
                      class="add-button"
                    >
                      +
                    </div>
                  </v-subheader>

                  <draggable
                    v-model="tasks2"
                    :options="{ group: 'people' }"
                    class="draggables"
                  >
                    <template v-for="task in tasks2">
                      <v-list-tile
                        :key="task.id"
                        class="task"
                        @click="
                          passValuesToDialog(task);
                          colName2 = columns[1].value;
                          preCol = columns[1].value;
                        "
                      >
                        <v-list-tile-content>
                          <div v-html="task.taskName"></div>
                          <div class="priority-container">
                            <div class="messages">
                              <font-awesome-icon
                                icon="fa-regular fa-message"
                                style="color: grey"
                              />
                              <div class="n-messages">
                                {{ task.nMessages }}
                              </div>
                            </div>
                            <div class="attach">
                              <font-awesome-icon
                                icon="fa-solid fa-link"
                                style="color: grey"
                              />
                              <div class="n-attach">
                                {{ task.nAttach }}
                              </div>
                            </div>
                            <div
                              class="priorityName"
                              :style="{
                                background: task.backClr,
                                color: task.txtClr,
                              }"
                              v-html="task.priorityName"
                            ></div>
                          </div>
                        </v-list-tile-content>
                      </v-list-tile>
                    </template>
                  </draggable>
                </v-list>
              </v-flex>

              <v-flex xs4 class="pa-3 ma-2">
                <v-list two-line class="each-col">
                  <v-subheader class="subheader">
                    In Review
                    <div class="counter">{{ tasks3.length }}</div>

                    <div
                      @click="
                        taskName = '';
                        description = '';
                        comments = '';
                        val = 'Low';
                        dialog = true;
                        colName = columns[2].value;
                      "
                      class="add-button"
                    >
                      +
                    </div>
                  </v-subheader>

                  <draggable
                    v-model="tasks3"
                    :options="{ group: 'people' }"
                    class="draggables"
                  >
                    <template v-for="task in tasks3">
                      <v-list-tile
                        :key="task.id"
                        class="task"
                        @click="
                          passValuesToDialog(task);
                          colName2 = columns[2].value;
                          preCol = columns[2].value;
                        "
                      >
                        <v-list-tile-content>
                          <div v-html="task.taskName"></div>
                          <div class="priority-container">
                            <div class="messages">
                              <font-awesome-icon
                                icon="fa-regular fa-message"
                                style="color: grey"
                              />
                              <div class="n-messages">
                                {{ task.nMessages }}
                              </div>
                            </div>
                            <div class="attach">
                              <font-awesome-icon
                                icon="fa-solid fa-link"
                                style="color: grey"
                              />
                              <div class="n-attach">
                                {{ task.nAttach }}
                              </div>
                            </div>
                            <div
                              class="priorityName"
                              :style="{
                                background: task.backClr,
                                color: task.txtClr,
                              }"
                              v-html="task.priorityName"
                            ></div>
                          </div>
                        </v-list-tile-content>
                      </v-list-tile>
                    </template>
                  </draggable>
                </v-list>
              </v-flex>
              <v-flex xs4 class="pa-3 ma-2">
                <v-list two-line class="each-col">
                  <v-subheader class="subheader">
                    Done
                    <div class="counter">{{ tasks4.length }}</div>

                    <div
                      @click="
                        taskName = '';
                        description = '';
                        comments = '';
                        val = 'Low';
                        dialog = true;
                        colName = columns[3].value;
                      "
                      class="add-button"
                    >
                      +
                    </div>
                  </v-subheader>

                  <draggable
                    v-model="tasks4"
                    :options="{ group: 'people' }"
                    class="draggables"
                  >
                    <template v-for="task in tasks4">
                      <v-list-tile
                        :key="task.id"
                        class="task"
                        @click="
                          passValuesToDialog(task);
                          colName2 = columns[3].value;
                          preCol = columns[3].value;
                        "
                      >
                        <v-list-tile-content>
                          <div v-html="task.taskName"></div>
                          <div class="priority-container">
                            <div class="messages">
                              <font-awesome-icon
                                icon="fa-regular fa-message"
                                style="color: grey"
                              />
                              <div class="n-messages">
                                {{ task.nMessages }}
                              </div>
                            </div>
                            <div class="attach">
                              <font-awesome-icon
                                icon="fa-solid fa-link"
                                style="color: grey"
                              />
                              <div class="n-attach">
                                {{ task.nAttach }}
                              </div>
                            </div>
                            <div
                              class="priorityName"
                              :style="{
                                background: task.backClr,
                                color: task.txtClr,
                              }"
                              v-html="task.priorityName"
                            ></div>
                          </div>
                        </v-list-tile-content>
                      </v-list-tile>
                    </template>
                  </draggable>
                </v-list>
              </v-flex>
            </v-layout>
          </v-row>
        </v-container>
      </v-content>
    </v-app>
  </div>
</template>
<script>
import draggable from "vuedraggable";
export default {
  name: "v-tabs",
  components: {
    draggable,
  },
  computed: {},
  methods: {
    generateRandomInteger(max) {
      return Math.floor(Math.random() * max) + 1;
    },

    passValuesToDialog(task) {
      this.val2 = task.priorityName;
      this.taskName2 = task.taskName;
      this.description2 = task.description;
      this.comments2 = task.comments;
      this.nowID = task.id;
      this.dialog2 = true;
    },
    setProperties(task) {
      task.priorityName = this.val2;
      if (task.priorityName == "Low") {
        task.backClr = this.priority[0].backColor;
        task.txtClr = this.priority[0].txtColor;
      } else if (task.priorityName == "Medium") {
        task.backClr = this.priority[1].backColor;
        task.txtClr = this.priority[1].txtColor;
      } else {
        task.backClr = this.priority[2].backColor;
        task.txtClr = this.priority[2].txtColor;
      }
      // pop then:
      if (this.preCol == "Backlog") {
        this.tasks.splice(this.tasks.indexOf(task), 1);
      } else if (this.preCol == "In Progress") {
        this.tasks2.splice(this.tasks2.indexOf(task), 1);
      } else if (this.preCol == "In Review") {
        this.tasks3.splice(this.tasks3.indexOf(task), 1);
      } else {
        this.tasks4.splice(this.tasks4.indexOf(task), 1);
      }
      task.colName = this.colName2;
      if (this.colName2 == "Backlog") {
        this.tasks.push(task);
      } else if (this.colName2 == "In Progress") {
        this.tasks2.push(task);
      } else if (this.colName2 == "In Review") {
        this.tasks3.push(task);
      } else {
        this.tasks4.push(task);
      }
      task.description = this.description2;
      task.taskName = this.taskName2;
      task.comments = this.comments2;
    },
    deleteTask() {
      let found = false;
      if (!found) {
        this.tasks.forEach((task) => {
          if (task.id == this.nowID) {
            found = true;
            this.tasks.splice(this.tasks.indexOf(task), 1);
          }
        });
      }
      if (!found) {
        this.tasks2.forEach((task) => {
          if (task.id == this.nowID) {
            found = true;
            this.tasks2.splice(this.tasks2.indexOf(task), 1);
          }
        });
      }
      if (!found) {
        this.tasks3.forEach((task) => {
          if (task.id == this.nowID) {
            found = true;
            this.tasks3.splice(this.tasks3.indexOf(task), 1);
          }
        });
      }
      if (!found) {
        this.tasks4.forEach((task) => {
          if (task.id == this.nowID) {
            found = true;
            this.tasks4.splice(this.tasks4.indexOf(task), 1);
          }
        });
      }

      this.dialog2 = false;
    },
    editElement() {
      let found = false;
      if (!found) {
        this.tasks.forEach((task) => {
          if (task.id == this.nowID) {
            found = true;
            this.setProperties(task);
          }
        });
      }
      if (!found) {
        this.tasks2.forEach((task) => {
          if (task.id == this.nowID) {
            found = true;
            this.setProperties(task);
          }
        });
      }
      if (!found) {
        this.tasks3.forEach((task) => {
          if (task.id == this.nowID) {
            found = true;
            this.setProperties(task);
          }
        });
      }
      if (!found) {
        this.tasks4.forEach((task) => {
          if (task.id == this.nowID) {
            found = true;
            this.setProperties(task);
          }
        });
      }

      this.dialog2 = false;
    },
    addElement() {
      let object = {
        id: 0,
        colName: "",
        taskName: "",
        priorityName: "",
        description: "",
        comments: "",
        txtClr: "",
        backClr: "",
        nMessages: "",
        nAttach: "",
      };
      object.nMessages = this.generateRandomInteger(40);
      object.nAttach = this.generateRandomInteger(20);
      object.backClr = this.backColor2;
      object.txtClr = this.txtColor2;
      this.id++;
      object.id = this.id;
      object.colName = this.colName;
      object.taskName = this.taskName;
      object.priorityName = this.val;
      object.description = this.description;
      object.comments = this.comments;
      if (object.colName == "Backlog") {
        this.tasks.push(object);
      } else if (object.colName == "In Progress") {
        this.tasks2.push(object);
      } else if (object.colName == "In Review") {
        this.tasks3.push(object);
      } else {
        this.tasks4.push(object);
      }
      this.dialog = false;
    },
  },
  mounted() {
    if (localStorage.getItem("id"))
      this.id = JSON.parse(localStorage.getItem("id"));
    if (localStorage.getItem("tasks"))
      this.tasks = JSON.parse(localStorage.getItem("tasks"));
    if (localStorage.getItem("tasks2"))
      this.tasks2 = JSON.parse(localStorage.getItem("tasks2"));
    if (localStorage.getItem("tasks3"))
      this.tasks3 = JSON.parse(localStorage.getItem("tasks3"));
    if (localStorage.getItem("tasks4"))
      this.tasks4 = JSON.parse(localStorage.getItem("tasks4"));
  },
  watch: {
    id: {
      handler() {
        localStorage.setItem("id", JSON.stringify(this.id));
      },
    },
    tasks: {
      handler() {
        localStorage.setItem("tasks", JSON.stringify(this.tasks));
      },
      deep: true,
    },
    tasks2: {
      handler() {
        localStorage.setItem("tasks2", JSON.stringify(this.tasks2));
      },
      deep: true,
    },
    tasks3: {
      handler() {
        localStorage.setItem("tasks3", JSON.stringify(this.tasks3));
      },
      deep: true,
    },
    tasks4: {
      handler() {
        localStorage.setItem("tasks4", JSON.stringify(this.tasks4));
      },
      deep: true,
    },
    val2: function (v) {
      if (this.val2 == "Low") {
        this.backColor3 = this.priority[0].backColor;
      } else if (this.val2 == "Medium") {
        this.backColor3 = this.priority[1].backColor;
      } else {
        this.backColor3 = this.priority[2].backColor;
      }
    },

    val: function (v) {
      if (this.val == "Low") {
        this.backColor2 = this.priority[0].backColor;
        this.txtColor2 = this.priority[0].txtColor;
      } else if (this.val == "Medium") {
        this.backColor2 = this.priority[1].backColor;
        this.txtColor2 = this.priority[1].txtColor;
      } else {
        this.backColor2 = this.priority[2].backColor;
        this.txtColor2 = this.priority[2].txtColor;
      }
    },
  },
  data() {
    return {
      // Separator for dialog 2
      preCol: "",
      colName2: "",
      val2: "",
      taskName2: "",
      description2: "",
      comments2: "",
      nowID: 0,

      // End of Separator
      backColor2: "#ddf7ec",
      txtColor2: "#34c784",
      backColor3: "#ddf7ec",
      val: "Low",
      dialog: false,
      dialog2: false,
      active: 0,
      id: -1,
      colName: "",
      taskName: "",
      description: "",
      comments: "",
      txtClr: "",
      backClr: "",

      columns: [
        {
          text: "Backlog",
          value: "Backlog",
        },
        {
          text: "In Progress",
          value: "In Progress",
        },
        {
          text: "In Review",
          value: "In Review",
        },
        {
          text: "Done",
          value: "Done",
        },
      ],
      priority: [
        {
          text: "Low",
          value: "Low",
          backColor: "#ddf7ec",
          txtColor: "#34c784",
        },
        {
          text: "Medium",
          value: "Medium",

          backColor: "#fff0d7",

          txtColor: "#f08b0d",
        },
        {
          text: "High",
          value: "High",

          backColor: "#ffe2e2",

          txtColor: "#ff5956",
        },
      ],
      tasks: [
        // {
        //   id: 1,
        //   taskName: "Create a profile screen",
        //   priorityName: "Medium",
        //   description: "",
        //   comments: "",
        //   txtClr: "#f08b0c",
        //   backClr: "rgb(249 217 163)",
        // },
      ],
      tasks2: [],
      tasks3: [],
      tasks4: [],
    };
  },
};
</script>
<style scoped>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  /* font-family: "Noto Sans", sans-serif !important; */
}
#app {
  position: relative;
}
.tri-holder {
  position: absolute;
  bottom: 100px;
  left: 0;
  z-index: 2;
}
.triangle {
  width: 0;
  height: 0;
  border-left: 50px solid transparent;
  border-right: 50px solid transparent;
  border-bottom: 100px solid #fe9008;
  position: relative;
  transform: rotate(-45deg);
}
.triangle:after {
  content: "";
  position: absolute;
  top: 5px;
  left: -45px;
  width: 0;
  height: 0;
  border-left: 45px solid transparent;
  border-right: 45px solid transparent;
  border-bottom: 92px solid rgb(245 248 253);
}
.bell {
  position: relative;
}
.bell::after {
  content: "";
  width: 14px;
  height: 14px;
  background-color: #2ccb87;
  border-radius: 50%;
  border: 2px solid white;
  position: absolute;
  z-index: 1000;
  top: 0;
  right: 0;
  margin-top: -4px;
  margin-right: -4px;
}
.circle-small,
.circle-medium,
.circle-big {
  border: 2px solid #fe9008;
  border-radius: 50%;
  position: absolute;
  z-index: 2;
  /* small */
  width: 30px;
  height: 30px;
}
.circle-small {
  bottom: 15px;
  right: 500px;
}
.circle-medium {
  width: 60px;
  height: 60px;
  top: 0;
  left: 100px;
}
.circle-big {
  width: 120px;
  height: 120px;
  top: 0;
  right: 0px;
  margin-top: -50px;
  margin-right: -50px;
}
.clear {
  clear: both;
}
.messages {
  position: absolute;
  font-size: 2.1vh;
  left: 0;
}
.n-messages,
.n-attach {
  display: inline-block;
  position: relative;
  font-size: 1.8vh;
  top: -0.2vh;
  font-weight: bold;
  left: 0.5vh;
}
.attach {
  position: absolute;
  font-size: 2.1vh;
  left: 22%;
}

.priorityName {
  border-radius: 5vh;
  direction: rtl;
  text-align: center;
  width: 5vw;
  font-size: 2vh;
  padding: 0.5vh 1.5vh;
  position: absolute;
  top: -0.5vh;
  right: 0;
}
.priority-container {
  position: relative;
  margin-top: 2vh;
  height: 3vh;
}
option {
  background-color: red;
}
.close-x {
  position: absolute;
  right: 5%;
  color: #fe2a2a;
  border-radius: 2vh;
  text-align: center;
  border: 2px solid #fe2a2a;
  width: 6vh;
  height: 6vh;
  line-height: 6vh;
  font-size: 2vh;
  cursor: pointer;
}
.close-x:hover {
  background-color: #fe2a2a;
  color: white;
}
.counter {
  display: inline-block;
  background-color: white;
  position: relative;
  font-size: 1.8vh;
  padding: 0;
  line-height: 3.5vh;
  padding-top: 0.2vh;
  color: #00a3ff;
  left: 5%;
  width: 5.5vh;
  text-align: center !important;
  border-radius: 2vh;
  box-shadow: 0px 3px 4px rgba(171, 171, 171, 0.288);
}
.add-button {
  display: inline-block;
  font-weight: normal;
  font-size: 3.5vh;
  color: grey;
  position: absolute;
  right: 8%;
  top: 50%;
  margin-top: -2.5vh;
  cursor: pointer;
}
.subheader {
  font-weight: bold;
  font-size: 1.5vw;
  color: #0a223d !important;
  position: relative;
  padding: 0;
  padding-left: 5%;
}
.each-col {
  height: 100%;
  background-color: #f0f4f9 !important;
  border-radius: 2.5vh !important;
  border-bottom-left-radius: 0 !important;
  border-bottom-right-radius: 0 !important;
  padding-bottom: 0;
}
.task {
  background-color: white;
  padding: 2.5vh;
  margin: auto;
  margin-bottom: 1vh;
  display: block;
  width: 95%;
  cursor: pointer;
  color: #0a223d;
  font-weight: bold;
  border-radius: 2vh;

  box-shadow: 0px 3px 6px rgba(171, 171, 171, 0.315);
}
.test {
  background-color: white;
  width: 100%;
  margin-bottom: -6vh;
  padding-left: 3vh;
  padding-top: 2vh;
  padding-right: 5vh;
}
.test2 {
  background-color: white;
  width: 100%;
  height: 11vh;
  font-weight: bold;
  font-size: 4vh;
  line-height: 11vh;
  padding-left: 3vh;
}
.columns-4 {
  height: 63vh;
  margin-top: -10vh;
}
.outer-body {
  background-image: linear-gradient(to right, #f5f8fd, #e5eefb);
}
.main-card {
  background-color: white;
  margin: 3vh 0;
  height: 90vh;
  overflow: hidden;
  position: relative;
  z-index: 10;
  border-radius: 3.5vh;
  box-shadow: 0px 0px 30px rgba(171, 171, 171, 0.329);
}
.draggables {
  height: 62vh;
  padding-bottom: 6vh;
  overflow-y: scroll;
}
/* width */
.draggables::-webkit-scrollbar {
  width: 3px;
}

/* Track */
.draggables::-webkit-scrollbar-track {
  border-radius: 10px;
}

/* Handle */
.draggables::-webkit-scrollbar-thumb {
  background: grey;
  border-radius: 10px;
}
</style>
