<template>
  <div class="container mt-4">
    <div class="row justify-content-md-center">
      <h1>MongoDB增刪改查</h1>
      <div class="col-3 mt-2 ml-5">
        <button class="btn btn-primary" v-on:click="student={}, addshow=true">增加</button>
        <button class="btn btn-primary" v-on:click="searchshow=true">搜索</button>
      </div>
      <div class="w-100"></div>
      <table class="table table-hover col-9">
        <thead>
          <tr>
            <th scope="col">ID</th>
            <th scope="col">姓名</th>
            <th scope="col">年龄</th>
            <th scope="col">性别</th>
            <th scope="col">年级</th>
            <th scope="col">学科</th>
            <th scope="col">学校</th>
            <th scope="col">
              <img src="../assets/set.png" alt width="22px" height="22px">
            </th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(todo, index) in content" :key="todo.id">
            <td scope="col">{{todo.id}}</td>
            <td scope="col">{{todo.name}}</td>
            <td scope="col">{{todo.age}}</td>
            <td scope="col">{{todo.sex}}</td>
            <td scope="col">{{todo.grade}}</td>
            <td scope="col">{{todo.department}}</td>
            <td scope="col">{{todo.school}}</td>
            <td scope="col">
              <button class="btn btn-primary" v-on:click="update(todo)">修改</button>&nbsp;
              <button
                class="btn btn-danger"
                v-b-modal.deletemodal
                v-on:click="remove(todo, index)"
              >删除</button>
            </td>
          </tr>
        </tbody>
      </table>
      <!--增加-->
      <b-modal hide-footer v-model="addshow" title="增加学生">
        <form v-on:submit.prevent>
          <div class="form-group row">
            <label for="staticEmail" class="col-sm-2 col-form-label">学号</label>
            <div class="col-sm-10">
              <input class="form-control" type="number" v-model="student.id">
            </div>
          </div>
          <div class="form-group row">
            <label class="col-sm-2 col-form-label">姓名</label>
            <div class="col-sm-10">
              <input class="form-control" v-model="student.name">
            </div>
          </div>
          <div class="form-group row">
            <label class="col-sm-2 col-form-label">年龄</label>
            <div class="col-sm-10">
              <input class="form-control" type="number" v-model="student.age">
            </div>
          </div>
          <div class="form-group row">
            <label class="col-sm-2 col-form-label">性别</label>
            <div class="col-sm-10">
              <b-form-radio-group
                id="radios"
                v-model="student.sex"
                class="mt-2"
                name="radioSubComponent"
              >
                <b-form-radio value="男">男</b-form-radio>
                <b-form-radio value="女">女</b-form-radio>
              </b-form-radio-group>
            </div>
          </div>
          <div class="form-group row">
            <label class="col-sm-2 col-form-label">年级</label>
            <div class="col-sm-10">
              <b-form-select v-model="student.grade">
                <option value="大一">大一</option>
                <option value="大二">大二</option>
                <option value="大三">大三</option>
                <option value="大四">大四</option>
              </b-form-select>
            </div>
          </div>
          <div class="form-group row">
            <label class="col-sm-2 col-form-label">学科</label>
            <div class="col-sm-10">
              <input class="form-control" v-model="student.department">
            </div>
          </div>
          <div class="form-group row">
            <label class="col-sm-2 col-form-label">学校</label>
            <div class="col-sm-10">
              <input class="form-control" v-model="student.school">
            </div>
          </div>
          <div slot="modal-footer" class="w-100 text-center">
            <button class="btn btn-danger" v-on:click="add()">确定增加</button>
          </div>
        </form>
      </b-modal>
      <!--修改-->
      <b-modal hide-footer class="p-4" v-model="updateshow" title="修改学生">
        <form v-on:submit.prevent>
          <div class="form-group row">
            <label for="staticEmail" class="col-sm-2 col-form-label">学号</label>
            <div class="col-sm-10">
              <input class="form-control" v-model="student.id" disabled>
            </div>
          </div>
          <div class="form-group row">
            <label class="col-sm-2 col-form-label">姓名</label>
            <div class="col-sm-10">
              <input class="form-control" v-model="student.name">
            </div>
          </div>
          <div class="form-group row">
            <label class="col-sm-2 col-form-label">年龄</label>
            <div class="col-sm-10">
              <input class="form-control" type="number" v-model="student.age">
            </div>
          </div>
          <div class="form-group row">
            <label class="col-sm-2 col-form-label">性别</label>
            <div class="col-sm-10">
              <b-form-radio-group id="radios" v-model="student.sex" name="radioSubComponent">
                <b-form-radio value="男">男</b-form-radio>
                <b-form-radio value="女">女</b-form-radio>
              </b-form-radio-group>
            </div>
          </div>

          <div class="form-group row">
            <label class="col-sm-2 col-form-label">年级</label>
            <div class="col-sm-10">
              <b-form-select v-model="student.grade">
                <option value="大一">大一</option>
                <option value="大二">大二</option>
                <option value="大三">大三</option>
                <option value="大四">大四</option>
              </b-form-select>
            </div>
          </div>

          <div class="form-group row">
            <label class="col-sm-2 col-form-label">学科</label>
            <div class="col-sm-10">
              <input class="form-control" v-model="student.department">
            </div>
          </div>
          <div class="form-group row">
            <label class="col-sm-2 col-form-label">学校</label>
            <div class="col-sm-10">
              <input class="form-control" v-model="student.school">
            </div>
          </div>
          <div slot="modal-footer" class="w-100 text-center">
            <button class="btn btn-danger" v-on:click="change()">确定修改</button>
          </div>
        </form>
      </b-modal>
      <!--删除modal-->
      <!-- Modal Component -->
      <b-modal id="deletemodal" @ok="handleOk" title="删除">
        <p class="my-4">确定删除{{student.name}}</p>
      </b-modal>
      <!--搜索-->
      <b-modal v-model="searchshow" title="搜索学生">
        <b-container>
          <form v-on:submit.prevent>
            <div class="form-group row" v-for="(todo, index) in selected[0]" :key="index">
              <b-form-select v-model="query.name" class="col-sm-2">
                <option
                  v-for="(i, index) in alltype"
                  :key="index"
                  width="10%"
                  :value="alltype[index]"
                >{{alltypecn[index]}}</option>
              </b-form-select>
              <div v-if="query.name != 'sex'" class="col-sm-10">
                <input class="form-control" v-model="query.value">
              </div>
              <div v-else class="col-sm-10">
                <b-form-radio-group
                  id="radios"
                  v-model="query.value"
                  class="mt-2"
                  name="radioSubComponent"
                >
                  <b-form-radio value="男">男</b-form-radio>
                  <b-form-radio value="女">女</b-form-radio>
                </b-form-radio-group>

                <!-- <input class="form-control" v-model="query.value"> -->
              </div>
            </div>
          </form>
        </b-container>
        <div slot="modal-footer" class="w-100 text-center">
          <b-btn size="sm" variant="primary" @click="querydata()">确定</b-btn>
        </div>
      </b-modal>
    </div>
  </div>
</template>
<script>
export default {
  name: "Main",
  data() {
    return {
      addshow: false,
      updateshow: false,
      searchshow: false,
      content: [],
      student: {},
      search: "",
      selected: [" "],
      alltypecn: ["学号", "姓名", "年龄", "性别", "年级", "学科", "学校"],
      alltype: ["id", "name", "age", "sex", "grade", "department", "school"],
      query: {}
    };
  },

  mounted() {
    this.axios.get("/api/student").then(body => {
      this.content = body.data;
      this.content.sort((a, b) => {
        return a.id - b.id;
      });
    });
  },
  methods: {
    update(student) {
      this.student = student;
      this.updateshow = true;
    },
    change() {
      this.axios.put("/api/student", this.student).catch(() => {
        alert("更新失败");
      });
      this.updateshow = false;
    },
    remove(todo, index) {
      this.student = todo;
      this.student.index = index;
    },
    add() {
      this.axios
        .post("/api/student", this.student)
        .then(() => {
          this.content.push(this.student);
          this.content.sort((a, b) => a.id - b.id);
        })
        .catch(() => {
          alert("添加失败");
        });
      this.addshow = false;
    },
    handleOk(evt) {
      // Prevent modal from closing
      this.axios
        .delete(`/api/student/${this.student.id}`)
        .then(() => {
          this.content.splice(this.student.index, 1);
        })
        .catch(() => {
          alert("删除失败");
        });
    },
    querydata() {
      this.axios
        .post("/api/student/query", this.query)
        .then(body => {
          this.content = body.data;
          this.content.sort((a, b) => a.id - b.id);
        })
        .catch(() => {});
      this.searchshow = false;
    }
  }
};
</script>