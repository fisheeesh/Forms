<template>
    <form @submit.prevent="Submit">

        <label for="">Email</label>
        <input type="email" required autocomplete="off" v-model="email" placeholder="name@gmail.com">

        <label for="">Password</label>
        <input type="password" required autocomplete="off" v-model="password" placeholder="abc123" :class="{pw : isErr}">
        <p v-if="errMsg" class="error">{{ errMsg }}</p>

        <label for="">Roles</label>
        <select v-model="role">
            <option disabled value="">Select a Role</option>
            <option value="Developer">Software Developer</option>
            <option value="Designer">Arthitecture Designer</option>
        </select>

        <div>
            <input type="checkbox" v-model="accept">
            <label for="">Accept Terms and Conditions</label>
        </div>

        <!-- <p>Choose Gender</p>
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
        </div> -->

        <div>
            <label for="">Skills</label>
            <input type="text" @keyup="addSkill" v-model="skill">
        </div>

        <div class="skillContainer">
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
    <p>Gender : {{ gender }}</p>
    <p>Skills : {{ skills }}</p>

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
            isErr: false
        }
    },
    methods: {
        addSkill(e) {
            console.log(e.key)
            if (e.key === "Alt" && this.skill) {
                this.skills.push(this.skill)
                this.skill = ""
            }
        },
        deleteSkill(skill) {
            this.skills = this.skills.filter(loopSkill => {
                return loopSkill != skill
            })
        },
        Submit() {
            if (this.password.length < 8) {
                this.errMsg = "Password must be at least 8 characters"
                this.isErr = true
            }
            else {
                console.log("Submitted")
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
    background: white;
    margin: 20px auto;
    border-radius: 10px;
    padding: 40px;
    text-align: left;
}

label {
    font-size: 0.6rem;
    text-transform: uppercase;
    font-weight: bold;
    letter-spacing: 1px;
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
}

input,
select {
    display: block;
    box-sizing: border-box;
    width: 100%;
    padding: 10px 6px;
    border: none;
    color: #555;
    border-bottom: 1px solid #ddd;
    transition: border-bottom 0.3s ease;
}
.pw{
    border-bottom: 1px solid red;
}

input[type="checkbox"] {
    display: inline-block;
    width: 16px;
    top: 2px;
    margin: 0 10px 0 0;
    position: relative;
}

input:focus,
select:focus {
    outline: none;
    border-bottom: 1px solid #aaa;
}

input::placeholder {
    color: #ddd;
}

.cross {
    color: red;
    margin-left: 10px;
    cursor: pointer;
}

.skillContainer {
    display: flex;
    flex-wrap: wrap;
}

.skill {
    display: inline-block;
    padding: 10px 15px;
    border: 1px solid #aaa;
    margin: 10px 2px 0px 2px;
    border-radius: 50px;
}

.align {
    margin-top: 30px;
    text-align: center;
}

button {
    border: none;
    background: royalblue;
    color: white;
    padding: 10px 20px;
    border-radius: 20px;
    cursor: pointer
}

.error {
    color: red;
    font-size: 0.6rem;
}
</style>