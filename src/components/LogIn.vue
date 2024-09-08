<template>
    <form>

        <label for="">Email</label>
        <input type="email" required autocomplete="off" v-model="email" placeholder="name@gmail.com">

        <label for="">Password</label>
        <input type="password" required autocomplete="off" v-model="password" placeholder="abc123">

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

        <p>Choose Gender</p>
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

    </form>

    <p>Email - {{ email }}</p>
    <p>Password - {{ password }}</p>
    <p>Role - {{ role }}</p>
    <p>Accept - {{ accept }}</p>
    <p>Gender : {{ gender }}</p>

</template>

<script>
export default {
    data() {
        return {
            email: "",
            password: "",
            role: "",
            accept : false,
            gender : []
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
</style>