<template>
    <div>
        <h1>protected page</h1>

        <form @submit.prevent="addBook">

            <input v-model="title"
            placeholder="Add book title"
            />

            <br>
            <input v-model="description"
            placeholder="Add book description"
            />

            <br>
            <input v-model="price"
            placeholder="Add book price"
            />
            <input v-model="author"
            placeholder="Add book author"
            />
            <input v-model="available"
            placeholder="Add book available"
            />
            <button on-submit="addBook">add book</button>

        </form>


        <br>

            <br>
            <br>
            <br>
            <br>
            <br>






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
