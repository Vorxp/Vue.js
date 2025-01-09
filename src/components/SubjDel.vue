<template>
  <button class="btn btn-sm btn-primary mx-2" 
  @click="editDetail(subId)">
    แก้ไขข้อมูล
  </button>
  <button class="btn btn-sm btn-danger mx-2"
   @click="delDetail(subId)">
    ลบข้อมูล
  </button>
</template>

<script>
export default {
  name: "SubjDel",
  props: ["subId"],
  data() {
    return {};
  },
  methods: {
    editDetail(theID) {
      this.$emit("edit", theID);
    },
    delDetail(theID) {
      fetch('http://localhost:3000/course/' +theID, {
        method: "DELETE"
      })
        .then(this.$emit('delete'))
        .catch();
    },
  },
};
</script>

<style>
</style>