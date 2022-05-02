<template>
    <div>
        <ul>
            <li v-for="menuItem in childMenuData" :key="menuItem.id" @click="curMenuId=menuItem.id">
            {{ menuItem.text }}
            </li>
        </ul>
    </div>
</template>

<script setup>

defineProps({
    'childMenuData': Array
})
</script>

<style scoped>

</style>