<template>
    <h1> home </h1>


    <div class="save-btn">
        <button @click="showModal = true">Save</button>
    </div>
    <SavedModal v-show="showModal" />
</template>

<script>
import SavedModal from '~/components/SavedModal.vue'

export default {
    components: { SavedModal },
    data() {
        return {
            showModal: false,
        }
    },
}
</script>
