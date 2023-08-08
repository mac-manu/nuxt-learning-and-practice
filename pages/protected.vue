<template>
    <div>
        <h1>protected page</h1>

        <input
            name="title"
            placeholder="Title"
            v-model="book.title"
            class="border-b pb-2 text-lg my-4 focus:outline-none w-full font-light text-gray-500 placeholder-gray-500 y-2"
        />
        <input
                name="description"
                placeholder="description"
                v-model="book.description"
                class="border-b pb-2 text-lg my-4 focus:outline-none w-full font-light text-gray-500 placeholder-gray-500 y-2"
        />

        <button @click="saveBook">Save book</button>


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
