<template>
 <div>
    <form action="POST" id="theform" @submit.prevent="handleSubmit">
    <label for="email">Email</label>
    <input type="email" requied v-model="email">
    <label for="password">Password</label>
    <input type="password" requied v-model="password">
    <div v-if="passwordError" class="error">{{ passwordError }}</div>
    <label for="role">Role</label>
    <select name="role" v-model="role">
        <option value="developer">Developer</option>
        <option value="designer">Designer</option>
    </select>
    <label for="skill">Skill</label>
    <input type="text" v-model="tempSkill" @keyup="addSkill">
    <div v-for="skill in skills" :key="skill" class="pill" >
    <span @click="removeSkill(skill)">{{ skill }}</span></div>
    <input type="checkbox" required v-model="terms" >
    <label for="conditons">ACCEPT TERMS AND CONDITIONS</label>
 
    <div class="submit">
        <button>Create an account</button>
    </div>
  </form>
  <p>{{ email }}</p>
  <p>{{ password }}</p>
  <p>{{ role }}</p>
 </div>
</template>

<script>
export default {
data(){
    return{
        email: null,
        password: null,
        role: null,
        terms: false,
        tempSkill: '',
        skills: [],
        passwordError:''
    }
},
methods:{
    addSkill(e){
        
        if(e.key === ',' && this.tempSkill){
            if(!this.skills.includes(this.tempSkill)){
                this.skills.push(this.tempSkill) 
            }
            this.tempSkill = ''
        }
    },
    removeSkill(skill){
       this.skills = this.skills.filter((element)=> {
            return skill !== element;
        }
        
        )
    },
    handleSubmit(){
        this.passwordError = this.password.length > 5 ? '' : 'Password must be at least 6 chars long'
    }
}
}
</script>

<style scoped>
form{
    min-width: 420px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
}
label{
    color: #aaa;
    display: inline-block;
    margin: 25px 0px 15px;
    font-size: 0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}
input,select{
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
    background: white;
}
input[type='checkbox']{
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top:2px;
    background: white;
    color: white;
}
button{
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
}
.submit{
    text-align: center;
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
.error{
    color: crimson;
    font-size: 12px;
}
</style>