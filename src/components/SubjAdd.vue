<template>
  <h3 class="alert">เพิ่มวิชา</h3>
  <div class="card">
    <div class="card-body">
      <form @submit.prevent="handleSubmit()">
        <div class="row">
          <div class="col-lg-2 col-md-4 col-sm-6 mt-2">
            <label for="subjId" class="form-label">รหัสวิชา</label>
            <input
              type="text"
              id="subjId"
              class="form-control"
              v-model.trim="subjs.id"
            />
          </div>
          <div class="col-lg-2 col-md-8 col-sm-6 mt-2">
            <label for="subjNameTh" class="form-label">ชื่อวิชาภาษาไทย</label>
            <input
              type="text"
              id="subjNameTh"
              class="form-control"
              v-model.trim="subjs.name"
            />
          </div>
          <div class="col-lg-2 col-md-8 col-sm-6 mt-2">
            <label for="subjName" class="form-label">ชื่อวิชาภาษาอังกฤษ</label>
            <input
              type="text"
              id="subjName"
              class="form-control"
              v-model.trim="subjs.nameeng"
            />
          </div>
          <div class="col-lg-2 col-md-4 col-sm-6 mt-2">
            <label for="subjId" class="form-label">หน่วยกิต</label>
            <input
              type="text"
              id="subjId"
              class="form-control"
              v-model.trim="subjs.credit"
            />
          </div>
          <div class="col-lg-2 col-md-3 col-sm-4 mt-2">
            <label for="stdGrade" class="form-label">เกรด</label>
            <select id="stdGrade" class="form-select" v-model="subjs.grade">
              <option value="A">A</option>
              <option value="B+">B+</option>
              <option value="B">B</option>
              <option value="C+">C+</option>
              <option value="C">C</option>
              <option value="D+">D+</option>
              <option value="D">D</option>
              <option value="F">F</option>
              <option value="W">W</option>
            </select>
          </div>
          <div class="col-lg-2 col-md-3 col-sm-4 mt-2">
            <label for="" class="form-label">ภาคการศึกษา</label>
            <div class="form-check">
              <input
                class="form-check-input"
                type="radio"
                id="stdsem"
                value="ภาคต้น"
                v-model="subjs.sem"
              />
              <label class="form-check-label" for="stdsem">ภาคต้น</label>
            </div>
            <div class="form-check">
              <input
                class="form-check-input"
                type="radio"
                id="stdsem"
                value="ภาคปลาย"
                v-model="subjs.sem"
              />
              <label class="form-check-label" for="stdsem">ภาคปลาย</label>
            </div>
          </div>
          <div class="mt-3">
            <button id="btnSubmit" type="submit" class="btn btn-dark save">
              Save!
            </button>
          </div>
        </div>
      </form>
    </div>
  </div>
  <div class="alert alert-success mt-2" v-show="addSuccess">
    Save วิชา "{{ subjs.name }}"" Complete!
  </div>
  <div class="alert alert-light-mt-2">
    รหัสวิชา: {{ subjs.id }} <br />
    ชื่อวิชา: {{ subjs.name }} <br />
    Subjectname: {{ subjs.nameeng }} <br />
    หน่วยกิต: {{ subjs.credit }} <br />
    Grade: {{ subjs.grade }} <br />
    ภาคการศึกษา: {{ subjs.sem }}
  </div>
</template>

<script>
export default {
  name: "SubjAdd",
  data() {
    return {
      subjs: {
        id: "",
        name: "",
        nameeng: "",
        credit: "",
        yr: 2565,
        grade: "",
        sem: "",
        isShow: false,
      },
      addSuccess: false,
      addError: false,
      errMessage: "",
    };
  },
  methods: {
    //Method ที่ทำงานเมื่อมีการ Submit
    handleSubmit() {
      let subjects = {
        SubjID: this.subjs.id,
        SubjNameTh: this.subjs.name,
        SubjName: this.subjs.nameeng,
        Credit: this.subjs.credit,
        year: this.subjs.yr,
        Grade: this.subjs.grade,
        Semester: this.subjs.sem,
        isShow: false,
      };

      fetch("http://localhost:3000/course", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(subjects),
      })
        .then(() => {
          this.addSuccess = true;
        })
        .catch((err) => {
          this.addError = true;
          this.errMessage = err;
        });
    },
  },
};
</script>

<style>
.btn,
.alert,
.col-lg-2{
  font-family: "Itim", cursive;
  font-weight: 400;
  font-style: normal;
}
.save{
   --b: 3px;   /* border thickness */
  --s: .45em; /* size of the corner */
  --color: #373B44;
   padding: calc(.5em + var(--s)) calc(.9em + var(--s));
  color: var(--color);
  --_p: var(--s);
  background:
    conic-gradient(from 90deg at var(--b) var(--b),#0000 90deg,var(--color) 0)
    var(--_p) var(--_p)/calc(100% - var(--b) - 2*var(--_p)) calc(100% - var(--b) - 2*var(--_p));
  transition: .3s linear, color 0s, background-color 0s;
  outline: var(--b) solid #0000;
  outline-offset: .6em;
  font-size: 16px;

  border: 0;

  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
}
.save:hover,
.save:focus-visible{
    --_p: 0px;
  outline-color: var(--color);
  outline-offset: .05em;
}
.save:active{
   background: var(--color);
  color: #fff;
}

</style>