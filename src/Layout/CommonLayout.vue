<template>
  <q-layout view="hHh lpR fFf">
    <SigmaHeader @toggle-drawer="toggleLeftDrawer" @toggle-theme="toggleTheme" :icon="icon" />
    <q-drawer v-model="leftDrawerOpen" side="left" bordered>
      <q-img src="../assets/profile-pic.jpg" />
      <div class="q-pa-md bg-grey-2 full-height">
        <q-list separator padding class=" text-black bg-grey-3">
          <q-item clickable v-ripple :to="menu.path" exact :active="link === menu.label" @click="link = menu.label"
            active-class="text-black bg-grey-2" v-for="menu, index of menuItems" :key="index">
            <q-item-section avatar>
              <q-icon outline color="teal" :name="menu.icon" />
            </q-item-section>
            <q-item-section>{{ menu.label }}</q-item-section>
            <q-item-section side>
              <q-icon name="chevron_right" color="teal" />
            </q-item-section>
          </q-item>
        </q-list>
        <div class="versionFooter text-caption text-center text-teal"> Version 0.0.1</div>
      </div>

    </q-drawer>

    <q-page-container>
      <div class="q-mt-lg q-pt-lg">
        
      <router-view />
      </div>
    </q-page-container>
    <!-- <SigmaFooter /> -->
  </q-layout>
</template>

<script>
import { ref, watch } from "vue";
// import SigmaFooter from "./Footer.vue";
import SigmaHeader from "./Header.vue";
export default {
  components: {
    // SigmaFooter,
    SigmaHeader,
  },
  setup() {
    const link = ref('Home');
    const menuItems = ref([
      {
        label: 'Home',
        path: '/',
        icon: 'home'
      },
      {
        label: 'categories',
        path: '/categories',
        icon: 'assignment'
      },
      {
        label: 'About',
        path: '/about',
        icon: 'info'
      }
    ]);
    const leftDrawerOpen = ref(false);
    const iconStatus = ref(false);
    const icon = ref("light_mode");

    const toggleLeftDrawer = () => {
      leftDrawerOpen.value = !leftDrawerOpen.value;
    };
    const toggleTheme = () => {
      iconStatus.value = !iconStatus.value;
    };
    watch(iconStatus, () => {
      iconStatus.value
        ? (icon.value = "light_mode")
        : (icon.value = "nightlight");
    });
    return {
      //variables
      leftDrawerOpen,
      iconStatus,
      icon,
      //functions
      toggleLeftDrawer,
      toggleTheme,
      menuItems,
      link
    };
  },
};
</script>
<style>
.versionFooter {
  position: fixed;
  bottom: 1%;
  left: 34%;
}
</style>
