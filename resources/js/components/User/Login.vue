<template>
    <div class="w-25 mt-3">
        <input v-model="email" type="email" class="form-control mb-2" placeholder="Email">
        <input v-model="password" type="password" class="form-control mb-2" placeholder="Password">
        <div v-if="error" class="text-danger mb-1">{{ this.error }}</div>
        <input @click.prevent="login" type="submit" class="btn btn-primary">
    </div>
</template>

<script>
export default {
    name: "Login",

    data() {
        return {
            email: null,
            password: null,
            error: null,
        }
    },



    methods: {
        login() {
            axios.post('/api/auth/login', {email: this.email, password: this.password})
            .then(res => {
                localStorage.access_token = res.data.access_token
                this.$router.push({ name: 'user.personal' })
            })
            .catch(err => {
                this.error = err.response.data.error;
            })
        }
    }

}
</script>

<style scoped>

</style>
