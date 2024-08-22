<script>
//การอ้างอิงใน script จะใช้ keyword: this
export default {
  name: 'App',
  //ฟังก์ชัน data จะส่งค่าในรูปแบบ Object นำไปใช้ใน template หรือส่วนอื่น ๆ ของ component ได้
  data() {
    return {
      firstName: "Chinnawat",
      lastName: "Suwanpasert",
      Nickname: '<i>Disk</i>',
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
    increment() {
      this.age++
    },
    //ฟังก์ชันลดอายุ
    decrement() {
      this.age--
    }
  }
}
</script>

<template>
  <!-- การอ้างอิงใน template จะใช้ interpolation {} -->
  <section>
    <!-- ตัวอย่างการผูก data 'picture' กับ attribute 'src' -->
    <img :src="picture" :width="size" :height="size" />
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
    <button @click="increment">Add Age</button>
    <button @click="decrement">Del Age</button>
  </section>
</template>

<style scoped></style>
