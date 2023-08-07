<template>
    <div>
        <h1>protected page</h1>
        <button @click="logout">Logout</button>
    </div>
</template>

<script setup>
definePageMeta({
    middleware: 'auth',
})

const supaAuth = useSupabaseAuthClient().auth

const logout = async () => {
    const { error } = await supaAuth.signOut();
    if (error) {
        alert(error.message);
    } else {
        return navigateTo('login');
    }

};
</script>
