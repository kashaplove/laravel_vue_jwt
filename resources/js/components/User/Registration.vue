<template>
    <div>
        <div class="w-25 mt-3">
            <input v-model="name" type="text" class="form-control mb-2" placeholder="Name">
            <input v-model="email" type="email" class="form-control mb-2" placeholder="Email">
            <input v-model="password" type="password" class="form-control mb-2" placeholder="Password">
            <input v-model="password_confirmation" type="password" class="form-control mb-2" placeholder="Confirm password">
            <div v-if="error" class="text-danger mb-1">{{ error }}</div>
            <input @click.prevent="store" type="submit" class="btn btn-primary">
        </div>
    </div>
</template>

<script>
export default {
    name: "Registration",

    data() {
        return {
            name: null,
            email: null,
            password: null,
            password_confirmation: null,
            error: null,
        }
    },

    mounted() {
        // console.log(localStorage.getItem('access_token'));
    },

    methods: {
        store() {
            axios.post('/api/users', {name: this.name, email: this.email, password: this.password, password_confirmation: this.password_confirmation})
            .then(res => {
                localStorage.setItem('access_token', res.data.access_token)
                this.$router.push({name: 'user.personal'})
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
