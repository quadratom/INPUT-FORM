<template>
  <form @submit.prevent="handleSubmit">
    <label>Email:</label>
    <input type="email" required v-model="email">

    <label>Password:</label>
    <input type="password" required v-model="password">
    <div if="passwordError" class="password">
      {{ passwordError }}
    </div>

    <label>Student Department:</label>
    <select v-model="role">
        <option value="Web Developer">Software Enginear</option>
        <option value="Data Science"> Data Scientise</option>
    </select>
     
    <label>Skills:</label>
    <input type="text" v-model="allSkill" @keyup.alt="addSkill">

    <div v-for="skill in skills" :key="skill" class="pill">
      <span @click="deleteSkill(skill)"> {{ skill }}</span>
    </div>
    
    <p>All Skill: {{ allSkill }}</p>

    <div class="term">
        <input type="checkbox" v-model="term">
        <label>Accept term and condition.</label>
    </div>

    <div class="submit">
      <button>
        Create Account
      </button>
    </div>

    <!-- <input type="checkbox" value="Moses"  v-model="name">
    <input type="checkbox" value="Leke" v-model="name">
    <input type="checkbox" value="Demeji" v-model="name"> -->

</form>
<p> Email: {{ email }}</p>
<p>Password: {{ password }}</p>
<p>Role: {{ role }}</p>
<p>Terms: {{ term }}</p>
<p>Name: {{ name }}</p>
</template>

<script>
export default {
    data() {
        return {
            email: '',
            password: '',
            role: 'Web Developer',
            term: false,
            // name: [],
            allSkill: '',
            skills: [],
            passwordError:''
        }
    },


    methods: {
      addSkill(e) {
        // console.log(e);
        if(e.key === ',' && this.allSkill){
          if(!this.skills.includes(this.allSkill)){
            this.skills.push(this.allSkill)
          }
          this.allSkill = ''
        }
      },
      deleteSkill(skill) {
        this.skills = this.skills.filter((item) => {
          return skill !== item
        })
      },
      handleSubmit() {
        // console.log('Form Submitted');
        this.passwordError = this.password.length > 5 ? '' : 'the password must be more than 6 characters'
      }
    } 
}
</script>

<style>
form {
  max-width: 420px;
  margin: 30px auto;
  background: white;
  text-align: left;
  padding: 40px;
  border-radius: 10px;
}
label {
  color: #aaa;
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.6em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}
input , select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}
input[type="checkbox"] {
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;
}
.pill {
  display: inline-block;
  margin: 20px 10px 0 0;
  padding: 6px 12px;
  background: #eee;
  border-radius: 20px;
  font-size: 12px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #777;
  cursor: pointer;
}
button  {
  background: #0b6dff;
  border: 0;
  padding: 10px 20px;
  margin-top: 20px;
  color: white;
  border-radius: 20px;
}
.submit {
  text-align: center;
}
</style>