<template>
    <form @submit.prevent="Submit">
        <label for="email">Email</label>
        <input type="email" id="email" required autocomplete="off" v-model="email" placeholder="name@gmail.com">

        <label for="password">Password</label>
        <input type="password" id="password" required autocomplete="off" v-model="password" placeholder="abc123" :class="{pw:isErr}">
        <p v-if="errMsg" class="error">{{ errMsg }}</p>

        <label for="">Roles</label>
        <select v-model="role">
            <option disabled value="">Select a role</option>
            <option value="developer">Software Developer</option>
            <option value="designer">Arthitecture Designer</option>
        </select>

        <div>
            <label for="">Skills</label>
            <input type="text" @keyup="addSkill" v-model="skill">
        </div>

        <div class="skillsContainer">
            <p class="skill" v-for="skill in skills" :key="skill">
                {{ skill }} <span class="cross" @click="deleteSkill(skill)"></span>
            </p>
        </div>
        <div>
            <input type="checkbox" v-model="accept">
            <label for="">Accept Terms and Conditions</label>
        </div>

        <div class="align">
            <button class="create">Create Account</button>
        </div>

    </form>

    <p>Email - {{ email }}</p>
    <p>Password - {{ password }}</p>
    <p>Role - {{ role }}</p>
    <p>Accept - {{ accept }}</p>
    <p>Gender - {{ gender }}</p>
    <p>Skills - {{ skills }}</p>

</template>

<script>
export default {
    data() {
        return {
            email: "name@gmail.com",
            password: "",
            role: "",
            accept: false,
            gender: [],
            skills: [],
            skill: "",
            errMsg: "",
            isErr : false
        }
    },
    methods: {
        addSkill(e) {
            // console.log(e.key)
            if (e.key === "Alt" && this.skill) {
                this.skills.push(this.skill)
                this.skill = ""
            }
        },
        deleteSkill(skill) {
            this.skills = this.skills.filter(loopskill => {
                return loopskill !== skill
            })
        },
        Submit() {
            if (this.password.length < 8) {
                this.errMsg = "Password must be at least 8 characters"
                this.isErr = true
            }
            else {
                console.log('submitted')
                this.isErr = false
                this.errMsg = ""
            }
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
    font-size: 0.6rem;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}

input,
select {
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
    transition: border-bottom 0.3s ease;
}

input[type="checkbox"] {
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;
}

input:focus,
select:focus {
    outline: none;
    border-bottom: 2px solid #aaa;
}

input::placeholder {
    color: #ddd;
}

.skillsContainer {
    display: flex;
    flex-wrap: wrap;
    gap: 5px;
}
.pw{
    border-bottom: 1px solid red;
    transition: border-bottom 1s ease;
}

.skill {
    display: inline-block;
    padding: 10px 15px;
    border: 1px solid #aaa;
    border-radius: 50px;
    margin: 10px 2px;
}

.cross {
    margin-left: 10px;
    color: red;
    font-size: 0.8rem;
}

.cross:hover {
    cursor: pointer;
}

.create {
    background-color: royalblue;
    padding: 15px 20px;
    color: white;
    border-radius: 10px;
    border: none;

}

.align {
    margin-top: 30px;
    text-align: center;
}
.error{
    font-size: 0.6rem;
    color: red;
}
</style>