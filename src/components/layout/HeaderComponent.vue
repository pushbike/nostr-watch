<template>
  <Disclosure as="nav" class="bg-gray-800" v-slot="{ open }">
    <!-- <div class="mx-auto max-w-none"> -->
    <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
      <div class="relative h-16 flex-none md:flex lg:flex items-center mx-3 justify-between">
        <div class="absolute inset-y-0 left-0  flex items-center sm:hidden">
        <!-- Mobile menu button-->
        <DisclosureButton class="inline-flex items-center justify-center rounded-md p-2 text-gray-400 hover:bg-gray-700 hover:text-white focus:outline-none focus:ring-2 focus:ring-inset focus:ring-white">
            <span class="sr-only">Open main menu</span>
            <Bars3Icon v-if="!open" class="block h-6 w-6" aria-hidden="true" />
            <XMarkIcon v-else class="block h-6 w-6" aria-hidden="true" />
        </DisclosureButton>
        </div>
        <span class="inline-block text-center text-slate-50 text-xl mt-4 md:mt-0">
          nostr.watch
          <sup class="relative -top-2" style="font-size: 0.6rem">{{ version }}</sup>
        </span>
        <div class="flex flex-1 items-center justify-center sm:items-stretch sm:justify-start">
          <div class="hidden sm:ml-6 md:block">
            <div class="flex space-x-4">
              
            <router-link 
              to="/relays"
              :active-class="`bg-white/25`"
              class="text-white hover:bg-white/25 px-3 py-2 rounded-md text-sm font-medium"
              >
              Relays
            </router-link>
            <a 
              href="https://github.com/dskvr/nostr-watch/issues/new/choose"
              target="_blank"
              class="text-white hover:bg-white/25 px-3 py-2 rounded-md text-sm font-medium"
            >
              Feedback
            </a>
            <a 
              href="https://github.com/dskvr/nostr-watch"
              target="_blank"
              class="text-white hover:bg-white/25 px-3 py-2 rounded-md text-sm font-medium"
            >
              Git
            </a>
            </div>
          </div>
        </div>

        <div class="absolute inset-y-0 right-0 flex items-center pr-2 sm:static sm:inset-auto sm:ml-6 sm:pr-0">
          <About />

          <DarkMode />
          
          <!-- Profile dropdown -->
          <Menu as="div" class="relative ml-3">
            <!-- <Menu as="div" class="relative ml-3"> -->
              <AuthComponent />
              <div v-if="store.user.getPublicKey">
              <MenuButton class="flex rounded-full bg-gray-800 text-sm focus:outline-none focus:ring-2 focus:ring-white focus:ring-offset-2 focus:ring-offset-gray-800">
                  <span class="sr-only">Open user menu</span>
                  <span class="text-white mt-1.5 mr-3 hidden md:block">{{ store.user.getNip05 || store.user.getName }}</span>
                  <img v-if="store.user.getPicture" class="h-8 w-8 rounded-full" :src="store.user.getPicture" alt="store.user.profile?.name" />
              </MenuButton>
              </div>
              <transition enter-active-class="transition ease-out duration-100" enter-from-class="transform opacity-0 scale-95" enter-to-class="transform opacity-100 scale-100" leave-active-class="transition ease-in duration-75" leave-from-class="transform opacity-100 scale-100" leave-to-class="transform opacity-0 scale-95">
              <MenuItems 
                style="z-index:9000 !important;" 
                class="absolute right-0 z-9000 mt-2 w-64 origin-top-right rounded-md bg-white dark:bg-slate-800 dark:border dark:border-slate-600 py-1 shadow-lg ring-1 ring-black ring-opacity-5 focus:outline-none">
                  <span v-if="store.user.getName" class="block text-ellipsis text-sm w-full font-extrabold mt-2">
                    {{ store.user.getName  }}
                  </span>  
                  <span v-if="store.user.getNip05" class="block text-ellipsis text-sm w-full mt-2">
                    {{ store.user.getNip05  }}
                  </span>  
                  <span class="block text-ellipsis text-xs mt-3 mb-2">
                    <code>{{ store.user.getPublicKey.slice(0, 16) }}...</code>
                  </span>  
                  <MenuItem v-slot="{ active }">
                  <a href="#" @click="signOut()" :class="[active ? 'bg-gray-100' : '', 'block px-4 py-2 text-sm text-gray-700']">Sign out</a>
                  </MenuItem>
              </MenuItems>
              </transition>
          </Menu>
          </div>
      </div>
    </div>

    <DisclosurePanel class="sm:hidden">
    <div class="space-y-1 px-2 pt-2 pb-3">
      <!-- <div class="block sm:ml-6 md:hidden">
              <div class="flex space-x-4"> -->
                
              <router-link 
                to="/relays"
           
                class="block text-white hover:bg-white/25 px-3 py-2 rounded-md text-sm font-medium"
                >
                Relays
              </router-link>
              <a 
                href="https://github.com/dskvr/nostr-watch/issues/new/choose"
                target="_blank"
                class="block text-white hover:bg-white/25 px-3 py-2 rounded-md text-sm font-medium"
              >
                Feedback
              </a>
              <a 
                href="https://github.com/dskvr/nostr-watch"
                target="_blank"
                class="block text-white hover:bg-white/25 px-3 py-2 rounded-md text-sm font-medium"
              >
                Git
              </a>
              <!-- <router-link to="/about">about</router-link>
              <a
                href="/" 
                
                :aria-current="item.current ? 'page' : undefined">
                  {{ item.name }}
              </a> -->
              <!-- </div>
          </div> -->
    </div>
    </DisclosurePanel>
</Disclosure>
</template>
<style scoped>
nav.menu {
  position:relative;
  z-index:10;
}
/* nav span,
nav.menu a {
  display: inline-block;
} */

nav.menu a { 
  text-decoration: none;
  margin: 0 22px 0 0;
  padding:5px 10px;
  color:#000;
  border-bottom: 1px dotted #999;
}

nav.menu a.active { 
  background:#000 !important;
  color: #fff;
  border: none;
}

nav.menu a:hover { 
  background: #f0f0f0;
}

</style>

<script>
import { Disclosure, DisclosureButton, DisclosurePanel, Menu, MenuButton, MenuItem, MenuItems } from '@headlessui/vue'
import { Bars3Icon, XMarkIcon } from '@heroicons/vue/24/outline'

import { defineComponent, defineAsyncComponent } from 'vue'
import { setupStore } from '@/store'
import UserLib from '@/shared/user-lib.js'

// import PreferencesComponent from '@/components/PreferencesComponent.vue'

const About = defineAsyncComponent(() =>
    import("@/components/partials/AboutNostrWatch.vue" /* webpackChunkName: "About" */)
);

const DarkMode = defineAsyncComponent(() =>
    import("@/components/partials/DarkMode.vue" /* webpackChunkName: "DarkMode" */)
);

const AuthComponent = defineAsyncComponent(() =>
    import("@/components/user/AuthComponent.vue" /* webpackChunkName: "AuthComponent" */)
);

import {version} from '../../../package.json'

export default defineComponent({
  title: "nostr.watch registry & network status",
  name: 'HeaderComponent',
  components: {
    // PreferencesComponent,
    AuthComponent,
    DarkMode,
    About,
    Disclosure, DisclosureButton, DisclosurePanel, Menu, MenuButton, MenuItem, MenuItems,
    Bars3Icon, XMarkIcon
  },
  data: function(){
    return {
      version: version
    }
  },
  props: {},
  setup(){
    return { 
      store : setupStore()
    }
  },
  created(){
  },
  mounted(){    
    this.store.layout.setActiveTab(this.$tabId)
  },
  unmounted(){
    // const activeId = this.store.layout.getActiveTab
    this.store.layout.deactivateTab(this.$tabId)
  },
  computed: {
  },
  methods: UserLib
});
</script>
