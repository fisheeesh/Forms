<template>
    <form @submit.prevent="Submit">

        <label for="">Email</label>
        <input type="email" autocomplete="off" placeholder="name@gmail.com" v-model="email">

        <label for="">Password</label>
        <input type="password" autocomplete="off" placeholder="abc123" v-model="password" :class="{pw : isError}" ref="pass">
        <p v-if="isError" class="error">{{ errMsg }}</p>

        <label for="">Role</label>
        <select v-model="role">
            <option disabled value="">Select A Role</option>
            <option value="Developer">Software Developer</option>
            <option value="Designer">Software Designer</option>
        </select>

        <!-- single checkbox -->
         <div>
            <input type="checkbox" v-model="accept">
            <label for="">Accept Terms and Conditions</label>
         </div>

         <!-- multiple checkboxes -->
          <label for="">Choose Gender</label>
          <div>
            <input type="checkbox" value="Male" v-model="gender">
            <label for="">Male</label>
          </div>
          <div>
            <input type="checkbox" value="Female" v-model="gender">
            <label for="">Female</label>
          </div>
          <div>
            <input type="checkbox" value="Gay" v-model="gender">
            <label for="">Gay</label>
          </div>
          <div>
            <input type="checkbox" value="Bisexual" v-model="gender">
            <label for="">Bisexual</label>
          </div>

          <div>
            <label for="">Skills</label>
            <input type="text" @keyup="addSkill" v-model="skill">
          </div>

          <div class="skillsContainer">
            <p v-for="skill in skills" :key="skill" class="skill">
                {{ skill }} <span class="cross" @click="deleteSkill(skill)">&#10006;</span>
            </p>
          </div>

          <div class="align">
            <button>Create Account</button>
          </div>

    </form>

    <p>Email - {{ email }}</p>
    <p>Password - {{ password }}</p>
    <p>Role - {{ role }}</p>
    <p>Accept - {{ accept }}</p>
    <p>Gender - {{ gender }}</p>

</template>

<script>
export default {
    data(){
        return{
            email : "name@gmail.com",
            password : "",
            role : "",
            accept : false,
            gender : [],
            skills : [],
            skill : "",
            errMsg : "",
            isError : false
        }
    },
    methods: {
        addSkill(e){
           if(e.key === "Enter" && this.skill){
            this.skills.push(this.skill)
            this.skill = ""
           }
        },
        deleteSkill(skill){
            this.skills = this.skills.filter((loopskill => loopskill != skill))
        },
        Submit(){
            if(this.password.length < 8){
                this.errMsg = "Password must be at least 8 characters"
                this.isError = true
                this.$refs.pass.focus()
            }
            else{
                console.log('submitted')
                this.isError = false
            }
        }
    }
}
</script>

<style>
form{
    max-width: 420px;
    background-color: white;
    margin: 30px auto;
    border-radius: 10px;
    padding: 30px;
    text-align: left;
}
label{
    font-size: 0.6rem;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
}
input, select{
    display: block;
    width: 100%;
    border: none;
    border-bottom: 1px solid #ddd;
    padding: 10px 6px;
    box-sizing: border-box;
    transition:  border-bottom 0.3s ease;
}
.pw{
    border-bottom: 2px solid crimson;
}
.pw:focus{
    border-bottom: 2px solid crimson;
}
input[type="checkbox"]{
    display: inline-block;
    width: 16px;
    top: 2px;
    position: relative;
    margin-right: 5px;
}
input:focus, select:focus{
    outline: none;
    border-bottom: 2px solid #aaa;
}
input::placeholder{
    color: #ddd;
}
.cross{
    color: crimson;
    margin-left: 10px;
    cursor: pointer;
}
.skillContainer{
    display: flex;
    flex-wrap: wrap;
}
.skill{
    display: inline-block;
    padding: 10px 15px;
    border: 1px solid #ddd;
    border-radius: 30px;
    margin: 10px 5px;
}
.align{
    text-align: center;
    margin-top: 30px;
}
button{
    border: none;
    background: royalblue;
    padding: 15px 20px;
    color: white;
    border-radius: 10px;
}
button:hover{
    opacity: 0.8;
    cursor: pointer;
}
.error{
    font-size: 0.6rem;
    color: crimson;
}

</style>