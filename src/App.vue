<script>
import { cloneVNode } from 'vue'
//การอ้างอิงใน script จะใช้ keyword: this
export default {
  name: 'App',
  //ฟังก์ชัน data จะส่งค่าในรูปแบบ Object นำไปใช้ใน template หรือส่วนอื่น ๆ ของ component ได้
  data() {
    return {
      firstName: "Chinnawat",
      lastName: "Suwanpasert",
      Nickname: '',
      day: 26,
      month: 12,
      year: 1996,
      age: 27,
      picture: "https://cdn-icons-png.flaticon.com/128/3135/3135715.png",
      size: 100,
      social: "https://www.facebook.com/ChinnawatDisk/",
      //การนิยาม data แบบ array
      hobby: ['Games', 'Guitar', 'Music', 'Movies'],
      //การนิยาม data แบบ object
      general: {
        gender: "ชาย",
        weight: 75,
        height: 175,
        status: false,
      }
    }
  },
  //methods คือ การกำหนดความสามารถอื่น ๆ ให้กับ component (ถ้าเขียนโดยใช้ methods ให้ระบุ keyword 'this' ด้านหน้า ตามด้วยชื่อ propoties ที่สนใจ )
  methods: {
    getFullName() {
      return `${this.firstName} ${this.lastName}`
    },
    getBirthDate() {
      return `${this.year}(TH ${(this.year + 543)})-${this.month}-${this.day}`
    },
    //ฟังก์ชั่นการทำงานของ event
    showData() {
      alert(this.firstName)
    },
    //ฟังก์ชันเพิ่มอายุ
    increment(value) {
      this.age += value
    },
    //ฟังก์ชันลดอายุ
    decrement(value) {
      this.age -= value
    },
    //ฟังก์ชันเพิ่มชื่อผ่าน input (Event Input)
    setNickName(event) {
      this.Nickname = event.target.value
    },
    //ฟังก์ชั่น alert การเพิ่มชื่อ (Event modifier)
    submitForm(e) {
      e.preventDefault() // คือ การแก้ปัญหาเมื่อกด submit แล้ว form จะ reset ค่าใน input โดยการเรียกใช้ function นี้จะทำให้ค่าใน Input ไม่ถูก reset ไป
      //alert("Nickname is saved")
      //การนำโครงสร้างของ img และ input element ที่อ้างอิงโดย ref มาแสดง
      console.log(this.$refs.imageEL)
      console.log(this.$refs.nickNameEL)
      //กำหนดให้ตัวแปร Nickname = element nickNameEL โดยนำค่า value มาแสดง (.value)
      this.Nickname = this.$refs.nickNameEL.value
    },
  }
}
</script>

<template>
  <!-- การอ้างอิงใน template จะใช้ interpolation {} -->
  <section>
    <!-- ตัวอย่างการผูก data 'picture' กับ attribute 'src' -->
    <!-- การอ้างอิงหรือเข้าถึง โครงสร้างของ element เพื่อนำไปใช้งาน ด้วย ref -->
    <img :src="picture" :width="size" :height="size" ref="imageEL" />
    <!-- Event Input -->
    <form @submit="submitForm">
      <label for="">Input Nickname</label>
      <!-- การอ้างอิงหรือเข้าถึง โครงสร้างของ element เพื่อนำไปใช้งาน ด้วย ref -->
      <input type="text" ref="nickNameEL" />
      <!-- <input type="text" v-on:input="setNickName" ref="nickNameEL" /> -->
      <button type="submit">Save</button>
    </form>
    <p>Name: {{ getFullName() }}</p>
    <p>Nickname: <span v-html="Nickname"></span></p>
    <p>Birthdate: {{ getBirthDate() }}</p>
    <p>Age: {{ age }}</p>
    <p>Social: <a :href="social" target="_blank">Fackbook</a></p>
    <!-- การแสดงผล data array ใน template -->
    <p>Hobby:</p>
    <ul>
      <li>{{ hobby[0] }}</li>
      <li>{{ hobby[1] }}</li>
      <li>{{ hobby[2] }}</li>
      <li>{{ hobby[3] }}</li>
    </ul>
    <!-- การแสดงผล data object ใน template -->
    <p>General Data</p>
    <ul>
      <li>Gender: {{ general.gender }}</li>
      <li>Weight: {{ general.weight }} kg.</li>
      <li>Height: {{ general.height }} cm.</li>
      <li>Status: {{ general.status }}</li>
    </ul>
    <!-- การใช้งาน event ใช้ v-on หรือ @ -->
    <button @click="showData">Click to alert</button>
    <!-- การใช้งาน Event Argumetn โดยส่ง Argument เป็น parameter ไปที่ Method increment ให้เพิ่มขึ้นทีละ 10 -->
    <!-- เพิ่ม event modifier ต่อจาก event โดยกำหนดให้คลิก ctrl + left click -->
    <button @click.ctrl="increment(10)">Add Age</button>
    <!-- การใช้งาน Event Argumetn โดยส่ง Argument เป็น parameter ไปที่ Method decrement ให้ลดลงทีละ 10 -->
    <!-- เพิ่ม event modifier ต่อจาก event โดยกำหนดให้คลิก scroll mouse -->
    <button @click.middle="decrement(10)">Del Age</button>
  </section>
</template>

<style scoped></style>
