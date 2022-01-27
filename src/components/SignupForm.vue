<template>
  <form @submit.prevent="handleSubmit">
    <label>Email: </label>
    <input type="email" name="" id="" v-model="email" required>
    <label>Password: </label>
    <input type="password" name="" id="" v-model="password" required>
    <div v-if="passwordError" class="error">{{passwordError}}</div>

    <label>Role:</label>
    <select v-model="role">
        <option value="developer">Web Developer</option>
        <option value="designer">Web Designer</option>
    </select>

    <label>Skills:</label>
    <input type="text" v-model="tempSkill" @keyup.alt="addSkill">
    <div v-for="skill in skills" :key="skill" class="pill">
        <span @click="deleteSkill(skill)">{{skill}}</span>
    </div>

    <div class="terms">
    <input type="checkbox" name="" id="" v-model="terms">
    <label>Accept terms and cond itions</label>
    </div>

    <div class="submit">
        <button @click="submitData">Create an Account</button>
    </div>
      
  </form>

    <div class="display">
        <div class="bind">
            <p>Email: {{email}} </p>
            <p>Password: {{password}} </p>
            <p>Role: {{role}} </p> 
            <p>Terms accepted: {{terms}} </p> 
        </div>
    </div>
    
    
</template>

<script>
export default {
    data() {
        return {
            email: "",
            password: "",
            role: "",
            terms: false,
            tempSkill: "",
            skills: [],
            passwordError: ''
        }
    },
    methods: {
        addSkill(e) {
            if(e.key === "," && this.tempSkill){
                if(!this.skills.includes(this.tempSkill)){
                    this.skills.push(this.tempSkill)
                }
                
                this.tempSkill = ""
                console.log(this.skills)
            }
        },
        deleteSkill(skill){
            this.skills = this.skills.filter(item => {
                return skill !== item
            })
        },
        handleSubmit(){
            //Handle password
            this.passwordError = this.password.length > 5 ? '':'Password must be 6 characters long'
            console.log(`Email: ${this.email}, Password: ${this.password}`)
        }
    }
}
</script>

<style>
    form {
        max-width: 600px;
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
        font-size: 0.8em;
        text-transform: uppercase;
        letter-spacing: 1.7px;
        font-weight: bold;
    }
    input, select {
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
    .pill{
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
    button {
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
    .error {
        color: #ff0e62;
        margin-top: 10px;
        font-size: 0.8em;
        font-weight: bold;
    }
    .display {
        max-width: 500px;
        margin: 30px auto;
        text-align: left;
    }
    
</style>