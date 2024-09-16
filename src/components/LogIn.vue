<template>
    <h2>LogIn Form</h2>
    <form @submit.prevent="Submit">
        <!-- Email Input -->
        <label>Email</label>
        <input type="email" placeholder="name@gmail.com" v-model="email" :class="{ red: EisErr }">
        <p v-if="EerrMsg" class="error">{{ EerrMsg }}</p>

        <!-- Password Input -->
        <label>Password</label>
        <input type="password" placeholder="abc123" v-model="password" :class="{ red: PisErr }">
        <p v-if="PerrMsg" class="error">{{ PerrMsg }}</p>

        <!-- Select Box -->
        <label>Role</label>
        <select v-model="role">
            <option disabled value="">Select a role</option>
            <option value="developer">Software Developer</option>
            <option value="designer">Software Designer</option>
        </select>

        <!-- Multiple Checkbox -->
        <div>
            <label>Gender</label>
            <div>
                <input type="checkbox" value="male" v-model="gender">
                <label>Male</label>
            </div>
            <div>
                <input type="checkbox" value="female" v-model="gender">
                <label>Female</label>
            </div>
            <div>
                <input type="checkbox" value="gay" v-model="gender">
                <label>Gay</label>
            </div>
            <div>
                <input type="checkbox" value="bisexual" v-model="gender">
                <label>Bisexual</label>
            </div>
        </div>

        <label>Skills</label>
        <input type="text" v-model="skill" @keydown.enter.prevent="addSkill">
        <div class="skillContainer">
            <p v-for="skill in skills" :key="skill" class="skill">
                {{ skill }} <span class="cross" @click="deleteSkill(skill)">&#10006;</span>
            </p>
        </div>

        <!-- Singel Checkbox -->
        <div>
            <input type="checkbox" v-model="accept">
            <label>Accept Terms and Conditions</label>
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
    <p>Skills - {{ skills }}</p>
</template>

<script>
import { ref, watch } from 'vue';

export default {
    setup() {
        let email = ref('')
        let password = ref('')
        let role = ref('')
        let accept = ref(false)
        let gender = ref([])
        let skill = ref('')
        let skills = ref([])
        let EisErr = ref(false)
        let PisErr = ref(false)
        let EerrMsg = ref('')
        let PerrMsg = ref('')

        // Watchers to clear error messages on valid input
        watch(email, (newValue) => {
            if (newValue !== '' && newValue.endsWith('@gmail.com')) {
                EisErr.value = false;
                EerrMsg.value = '';
            }
        });

        watch(password, (newValue) => {
            if (newValue.length >= 8) {
                PisErr.value = false;
                PerrMsg.value = '';
            }
        });


        let addSkill = () => {
            if (!skills.value.includes(skill.value) && skill.value) {
                skills.value.push(skill.value)
                skill.value = ''
            }
            else skill.value = ''
        }

        let deleteSkill = (skill) => {
            skills.value = skills.value.filter(s => s !== skill)
        }

        let Submit = () => {
            // Initialize error flags and messages
            EisErr.value = false;
            PisErr.value = false;
            EerrMsg.value = '';
            PerrMsg.value = '';

            // Email validation
            if (email.value === '' || !email.value.endsWith('@gmail.com')) {
                EisErr.value = true;
                EerrMsg.value = 'Invalid Email. Please enter a valid email!';
            }

            // Password validation
            if (password.value.length < 8) {
                PisErr.value = true;
                PerrMsg.value = 'Password must be at least 8 characters';
            }

            // If there are no errors, proceed with form submission
            if (!EisErr.value && !PisErr.value) {
                console.log('submitted');
                // Handle successful submission here
            }
        }

        return { email, password, role, accept, gender, skills, addSkill, skill, deleteSkill, Submit, EisErr, EerrMsg, PerrMsg, PisErr }
    }
}
</script>

<style>
form {
    max-width: 620px;
    background: white;
    padding: 40px;
    margin: 10px auto;
    border-radius: 10px;
    text-align: left;
}

label {
    display: inline-block;
    text-transform: uppercase;
    font-size: 0.6rem;
    font-weight: bold;
    letter-spacing: 1px;
    color: #aaa;
    margin: 25px 0 5px 0;
}

input,
select {
    display: block;
    padding: 10px 5px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    outline: none;
    margin-top: 10px;
    transition: border-bottom 0.5s;
}

input[type="checkbox"] {
    display: inline-block;
    width: 16px;
    position: relative;
    top: 2px;
}

input::placeholder {
    color: #ddd;
}
.red:focus{
    border-bottom: 1px solid red;
}

input:focus {
    border-bottom: 1px solid #222;
}

.cross {
    color: red;
    margin-left: 15px;
    cursor: pointer;
}

.skill {
    border: 1px solid black;
    display: inline-block;
    padding: 10px 15px;
    margin: 5px;
    border-radius: 15px;
}

button {
    background: royalblue;
    color: #ddd;
    padding: 15px 20px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background 0.3s ease;
}

button:hover {
    background: rgb(43, 81, 192);
}

.align {
    text-align: center;
    margin-top: 20px;
}

.error {
    font-size: 0.6rem;
    color: red;
}
</style>