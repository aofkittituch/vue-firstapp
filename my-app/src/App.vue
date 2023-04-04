<template>
  <section>
    <img
      :src="picture"
      alt="profile-picture"
      :width="size"
      ref="imageEl"
    /><br />
    <h1>ชื่อผู้สมัคร : {{ getFullname }}</h1>
    <h1>age : {{ age }}</h1>
    <h1>salary : {{ salary }} THB</h1>
    <h1>salary per year : {{ getIncome }} THB</h1>
    <h1>ตำแหน่งงาน : {{ getPosition }}</h1>
    <button @click="addSalary(5000)">เพิ่มเงินเดือน</button>
    <button @click="toggleVisible">
      {{ isVisible ? "hide" : "show" }}detail
    </button>
    <article v-show="isVisible">
      <p><span v-html="address"></span></p>
      <p>social : <a :href="social" target="_blank">Facebook</a></p>
      <p v-if="hobby.length === 0">no hobby</p>
      <div v-else>
        <p>hobby :</p>
        <ul>
          <li v-for="(item, index) in hobby" :key="index">{{ item }}</li>
        </ul>
      </div>
      <p>personal data :</p>
      <ul>
        <li v-for="(item, key) in general" :key="key">
          {{ key }} : {{ item }}
        </li>
      </ul>
    </article>
  </section>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      firstname: "test",
      lastname: "studio",
      nickname: "",
      age: 15,
      address: "<i>กรุงเทพ</i>",
      picture: "https://cdn-icons-png.flaticon.com/512/456/456212.png",
      size: 50,
      social: "https://www.flaticon.com/",
      hobby: ["a", "b", "c", "d", "e"],
      general: { gender: "men", weight: 80, height: 179, status: false },
      isVisible: false,
      salary: 20000,
    };
  },
  methods: {
    toggleVisible() {
      this.isVisible = !this.isVisible;
    },
    addSalary(value) {
      this.salary += value;
    },
  },
  computed: {
    getFullname() {
      return `${this.firstname} ${this.lastname}`;
    },
    getIncome() {
      return this.salary * 12;
    },
    getPosition() {
      return this.salary >= 35000 ? "Project Manager" : "Programmer";
    },
  },
  watch: {
    salary(value) {
      if (value > 50000) {
        alert("เงินเดือนไม่ควรเกิน 50000 บาท");
        setTimeout(() => {
          this.salary = 50000;
        }, 100);
      }
    },
  },
};
</script>

<style></style>
