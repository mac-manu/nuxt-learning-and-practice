<template>
    <div>
        <h1>Registed page</h1>
        <form @submit.prevent="login">
            <input v-model="credentials.email" type="email" placeholder="Email" />
            <input v-model="credentials.password" type="password" placeholder="Password" />
            <button type="submit">Registed</button>
        </form>
    </div>
</template>


<script setup>
definePageMeta({
    middleware: 'unauth',
});

// create a user and login
const supaAuth = useSupabaseAuthClient().auth

const credentials = reactive({
    email: '',
    password: ''
})

const registed = async () => {
    const { error } = await supaAuth.signUp(credentials)

    if (error) {
        alert(error.message);
    } else {
        return navigateTo('/');
    }
}


</script>
