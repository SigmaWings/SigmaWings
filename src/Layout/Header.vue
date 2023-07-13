<template>
  <q-header bordered class="bg-grey-1 text-white mobile-only">
    <!-- <q-toolbar> -->
    <div class="row q-px-md items-center">
      <div class="col-3">
        <q-btn dense flat round icon="menu" @click="toggleDrawerEmits" color="black" />
      </div>
      <div class="col-6">
        <div class="row items-center justify-center text-black">
          <div class="text-h6">SIGMA</div>
          <q-img src="../assets/pngtree-wings-logo-png-image_6554013.png" style="height: 40px; max-width: 80px" />
        </div>
      </div>
      <div class="col-3 text-right"> 
        <!-- <q-icon name="info" color="red" /> -->
        <q-icon name="notifications" color="grey" size="sm">
      </q-icon>
      </div>
    </div>
    <div class="q-px-md q-mb-md q-mt-sm">
      <q-input label="Search" dense  outlined v-model="text">
      <template v-slot:prepend>
        <q-icon name="search" />
      </template>
    </q-input>
    </div>
    
    <!-- <q-btn :icon="icon" flat @click="toggleThemeEmits" />
      <q-toolbar-title> Sigma-Wings </q-toolbar-title> -->

    <!-- </q-toolbar> -->
  </q-header>
  <q-header bordered class="bg-grey-1 text-black desktop-only">
    <div class="row items-center">
      <div class="col">
        <q-tabs no-caps class="text-black ">
          <q-route-tab v-for="menu, index of menuItems" :key='index' :to="menu.path" exact replace :label="menu.label" />
        </q-tabs>
      </div>
      <div class="col text-center">
        <div class="row items-center justify-center">
          <div class="text-h6">SIGMA</div>
          <q-img src="../assets/pngtree-wings-logo-png-image_6554013.png" style="height: 40px; max-width: 110px" />
        </div>
      </div>
      <q-separator vertical />
      <div class="col">
        <div class="row justify-end items-center">
          <q-input label="Search" dense borderless v-model="text">
            <template v-slot:prepend>
              <q-icon name="search" />
            </template>
          </q-input>

          <q-img src="../assets/profile-pic.jpg" style="height: 50px; max-width: 50px" />
        </div>
      </div>
    </div>

    <!-- <q-toolbar>
      <q-toolbar-title class="text-center">
        <q-avatar>
          <img src="https://cdn.quasar.dev/logo-v2/svg/logo.svg">
        </q-avatar>
        Quasar Framework
      </q-toolbar-title>
    </q-toolbar> -->
  </q-header>
</template>

<script>
import { ref } from "vue";
export default {
  name: "SigmaHead",
  emits: ["toggleDrawer", "toggleTheme"],
  props: ["icon"],
  setup(props, context) {
    const menuItems = ref([
      {
        label: 'Home',
        path: '/'
      },
      {
        label: 'categories',
        path: '/categories'
      },
      {
        label: 'About',
        path: '/about'
      }
    ])

    const toggleDrawerEmits = (e) => {
      context.emit("toggleDrawer", e.target.value);
    };
    const toggleThemeEmits = (e) => {
      context.emit("toggleTheme", e.target.value);
    };
    function navDelay(e, go) {
      e.preventDefault() // we cancel the default navigation

      // console.log('triggering navigation in 2s')
      setTimeout(() => {
        // console.log('navigating as promised 2s ago')
        go()
      }, 2000)
    }

    function navCancel(e) {
      e.preventDefault() // we cancel the default navigation
    }

    function navRedirect(e, go) {
      e.preventDefault() // we cancel the default navigation

      // call this at your convenience
      go({
        to: { query: { tab: '2', noScroll: true } },
        // replace: boolean; default is what the tab is configured with
        // returnRouterError: boolean; default is false
      })
      // .then(vueRouterResult => { /* ... */ })
      // .catch(vueRouterError => {
      //   /* ...will not reach here unless returnRouterError === true */
      // })
    }

    function navPass() { }
    return {
      toggleDrawerEmits,
      toggleThemeEmits,
      navDelay, navCancel, navRedirect, navPass,
      menuItems
    };
  },
};
</script>
