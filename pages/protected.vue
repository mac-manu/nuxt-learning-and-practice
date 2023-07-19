<template>
    <div>
        <h1>protected page</h1>
    </div>
</template>

<script setup>
definePageMeta({
    middleware: 'auth',
})
</script>
