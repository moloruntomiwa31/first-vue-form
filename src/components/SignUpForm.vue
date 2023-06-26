<template>
    <form @submit.prevent="createAccount">
        <label for="email">Email Address: </label>
        <input type="email" required v-model="email">

        <label for="email">Password: </label>
        <input type="password" required v-model="password">
        <div v-if="passwordError" class="error">{{ passwordError }}</div>

        <label for="Role">Role</label>
        <select v-model="role">
            <option value="designer">Designer</option>
            <option value="developer">Developer</option>
        </select>

        <label for="">Skills</label>
        <input type="text" v-model="tempSkill" @keyup="addSkill">
        <div v-for="(skill, index) in skills" :key="index" class="pill">
            <p @click="deleteSkill(index)">{{ skill }}</p>
        </div>

        <div class="terms">
            <input type="checkbox" required v-model="terms">
            <label for="">Accept terms</label>
        </div>

        <div class="btn">
            <button>Create an Account</button>
        </div>
    </form>
</template>

<script>
export default {
    data() {
        return {
            email: ' ',
            password: "",
            role: "designer",
            terms: false,
            skills: [],
            tempSkill: "",
            passwordError: ""
        }
    },
    methods: {
        addSkill(e) {
            if (e.key === "Enter" && this.tempSkill) {
                if (!this.skills.includes(this.tempSkill)) {
                    this.skills.push(this.tempSkill)
                }
                this.tempSkill = ""
            }
        },
        deleteSkill(index) {
            this.skills.splice(index, 1)
        },
        createAccount() {
           this.passwordError = this.password.length > 5 ? " " : "Password must be at least 6 characters"
        }
    }
}
</script>
<style>
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
        font-family: Poppins;
    }
    body {
        background-color: rgb(253, 241, 187);
        height: 100vh;
        width: 100%;
        padding: 20px;
    }
    form {
        background-color: bisque;
        margin: 20px;
        padding: 20px;
        height: 100%;
        border-radius: 15px;
    }
    label{
        text-transform: uppercase;
        font-weight: bold;
        display: block;
        padding: 8px;
    }
    input, select {
        padding: 10px;
    }
    .terms {
        display: flex;
        align-items: center;
        justify-content: center;
    }
    .pill {
        background-color: white;
        color: black;
        width: fit-content;
        padding: 5px;
        display: block;
        margin: 5px;
        border-radius: 7px;
        cursor: pointer;
    }
    .btn {margin: 10px;}
    .btn button {
        padding: 10px;
        border: none;
        color: white;
        background-color: blue;
        border-radius: 15px;
    }
    .error {
        color: red;
    }
</style>