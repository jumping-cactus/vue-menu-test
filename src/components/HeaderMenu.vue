<template>
  <img alt="Vue logo" class="logo" src="../assets/logo.svg" width="125" height="125" />
  <ul>
    <li v-for="menuItem in rootMenuItems" :key="menuItem.id" @click="menuClick(menuItem.id)">
      {{ menuItem.text }}
    </li>
  </ul>
  <SideMenu v-if="hideSideMenu" :childMenuData=filteredMenu />
</template>



<script setup>
import { ref, computed } from "vue";
import SideMenu from "./SideMenu.vue";

const menuData = ref([
  { id: 900123, text: "Services", parent: 0 },
  { id: 900124, text: "Admin", parent: 0 },
  { id: 900125, text: "Search", parent: 0 },
  { id: 900126, text: "My Services", parent: 900123 },
  { id: 900127, text: "New Service", parent: 900123 },
  { id: 900128, text: "Modify Service", parent: 900123 },
  { id: 900129, text: "ABC", parent: 900124 },
  { id: 900130, text: "EFG", parent: 900124 },
  { id: 900131, text: "XYZ", parent: 900124 },
]);

const curMenuId = ref(900123)
const hideSideMenu = ref(false)

const rootMenuItems = computed(() => {
  return menuData.value.filter((menuItem) => menuItem.parent === 0);
});

const filteredMenu = computed(() => {
  return menuData.value.filter((menuItem) => menuItem.parent === curMenuId.value);
});

const menuClick = (menuItemId) => {
    // console.log(menuItemId)
    // always show if clicking on new parent menu item
    if ( curMenuId.value !== menuItemId ) {
        hideSideMenu.value = true
    } else {
        hideSideMenu.value = !hideSideMenu.value
    }

    curMenuId.value = menuItemId

    
}


</script>




<style scoped>
li {
    display: inline-flex;
    padding: 0 10px;
    cursor: pointer;
}
li:hover {
    background-color: rgb(63, 63, 63);
}
</style>