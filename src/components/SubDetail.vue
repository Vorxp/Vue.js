<template>
    <div>
        <div class="card my-2">
            <div class="card-body bg-info bg-opacity-10">
                <h5 class="card-title">รหัสวิชา {{ subject.id }}</h5>
                <div class="card-sub-title">ชื่อวิชา {{ subject.name }}</div>
                <div class="cart-text">เกรดวิชา {{ subject.grade }} หน่วยกิต {{ subject.credit }}</div>
            </div>
        </div>
        <button class="btn btn-success" @click="editDetail">
            แก้ไขข้อมูล
        </button>
        &nbsp;
        <button class="btn btn-success" @click="delDetail(stdId)">
            ลบข้อมูล
        </button>
        <!-- เพิ่มส่วนนี้เพื่อเรียกใช้ SubjEdit.vue -->
        <div v-if="isEdit">
            <SubjEdit :stdId="stdId" />
        </div>
    </div>
</template>

<script>
import SubjEdit from './SubjEdit.vue'; // Import SubjEdit component

export default {
    name: 'SubDetail',
    props: ['stdId'],
    data() {
        return {
            subject: [],
            isEdit: false
        };
    },
    mounted() {
        this.fetchStudentData();
    },
    methods: {
        fetchStudentData() {
            fetch(`http://localhost:3000/subject/${this.stdId}`)
                .then(res => res.json())
                .then(data => this.subject = data)
                .catch(err => console.log(err.message))
        },
        editDetail() {
            this.isEdit  =!this.isEdit;
        },
        delDetail(theId) {
            fetch(`http://localhost:3000/course/${theId}`, {
          method: 'DELETE',
        })
          .then(() => {
            this.Subject = this.Subject.filter((subj) => subj.id !== theId);
          })
          .catch((err) => console.error('Delete Error:', err));

        }
    },
    components: {
        SubjEdit // Register SubjEdit component
    }
};
</script>

<style>
/* Add your styles here */
</style>