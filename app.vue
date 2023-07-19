<template>
  <div>
       <NuxtLink to="/">
          Home
      </NuxtLink>
      <NuxtLink to="/data">
          Data
      </NuxtLink>
      <div v-if="!user">
        <NuxtLink to="/login">
            Login
        </NuxtLink>
      </div>
      <div v-else>
        <NuxtLink to="/protected">
            Protected page
        </NuxtLink>
      </div>


    <NuxtPage />
  </div>
</template>

<script setup>
  const user = useSupabaseUser()
</script>
