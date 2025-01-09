<template>
  <div class="col" style="padding: 12px 0px">
    <li v-for="(subj, SubjID) in Subject" :key="SubjID" class="list-point">
      <div style="padding-bottom: 8px">
        <div style="border: 2px solid Tomato" class="card">
          <div class="row" style="padding: 20px">
            <div class="col-2 col-md-2 grade_detail">
              <span style="font-weight: 600"> {{ subj.SubjID }} </span>
            </div>

            <div class="col-4 col-md-2 grade_detail grade_center">
              <span>{{ subj.Credit }} หน่วยกิต</span>
            </div>

            <div class="col-8 col-md-3 border_grade">
              <p class="grade_Text_600" style="margin-bottom: 0px">
                {{ subj.SubjNameTh }}
              </p>
              <span class="grade_subject"> {{ subj.SubjName }} </span>
            </div>

            <div class="col-4 col-md-3 grade_year">
              <p class="grade_Text_600" style="margin-bottom: 0px">
                ปีการศึกษา {{ subj.year }}
              </p>
              <span class="grade_yr"> {{ subj.Semester }} </span>
            </div>

            <div class="col-2 col-md-2 grade_char">
              <span> {{ subj.Grade }} </span>
            </div>
          </div>
        </div>
      </div>

      <div>
        <button
          @click="deleteSubject(subj.id)"
          class="btn btn-danger btn-sm delete"
        >
          ลบ
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="16"
            height="16"
            fill="currentColor"
            class="bi bi-arrow-up"
            viewBox="0 0 16 16"
          >
            <path
              fill-rule="evenodd"
              d="M8 15a.5.5 0 0 0 .5-.5V2.707l3.146 3.147a.5.5 0 0 0 .708-.708l-4-4a.5.5 0 0 0-.708 0l-4 4a.5.5 0 1 0 .708.708L7.5 2.707V14.5a.5.5 0 0 0 .5.5"
            />
          </svg>
        </button>
      </div>
    </li>
  </div>
</template>

<script>
export default {
  name: "SubjList",
  components: {},
  data() {
    return {
      Subject: [],
    };
  },
  mounted() {
    fetch("http://localhost:3000/course")
      .then((res) => res.json())
      .then((data) => (this.Subject = data))
      .catch((err) => console.log(err.message));
  },
  methods: {
    showEdit(theSubjID) {
      this.editId = theSubjID;
      this.isEdit = true;
    },
    reload() {
      this.$parent.showStdList = !this.$parent.showStdList;
    },
    deleteSubject(SubjID) {
      if (confirm("คุณต้องการลบรายการนี้ใช่หรือไม่?")) {
        fetch(`http://localhost:3000/course/${SubjID}`, {
          method: "DELETE",
        })
          .then(() => {
            this.Subject = this.Subject.filter((subj) => subj.id !== SubjID);
          })
          .catch((err) => console.error("Delete Error:", err));
      }
    },
  },
};
</script>

<style>
.grade_detail,
.border_grade,
.grade_year,
.grade_char,
.delete {
  font-family: "Itim", cursive;
  font-weight: 400;
  font-style: normal;
}
.list-point {
  list-style-type: none;
  margin-left: 50px;
  margin-right: 50px;
  border-radius: 10px;
}

.delete {
  --b: 3px; /* border thickness */
  --s: 0.45em; /* size of the corner */
  --color: #373b44;
  padding: calc(0.5em + var(--s)) calc(0.9em + var(--s));
  color: var(--color);
  --_p: var(--s);
  background: conic-gradient(
      from 90deg at var(--b) var(--b),
      #0000 90deg,
      var(--color) 0
    )
    var(--_p) var(--_p) / calc(100% - var(--b) - 2 * var(--_p))
    calc(100% - var(--b) - 2 * var(--_p));
  transition: 0.3s linear, color 0s, background-color 0s;
  outline: var(--b) solid #0000;
  outline-offset: 0.6em;
  font-size: 16px;

  border: 0;

  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
}
.delete:hover,
.delete:focus-visible {
  --_p: 0px;
  outline-color: var(--color);
  outline-offset: 0.05em;
}
.delete:active {
  background: var(--color);
  color: #fff;
}
</style>