<script setup>
import { computed } from "vue";
import { useStore } from "vuex";
import { activateDarkMode, deactivateDarkMode } from "@/assets/js/dark-mode";

const store = useStore();
// state
const isRTL = computed(() => store.state.isRTL);
const isNavFixed = computed(() => store.state.isNavFixed);
const toggleConfigurator = () => store.commit("toggleConfigurator");

// mutations
const navbarFixed = () => store.commit("navbarFixed");
const setSidebarType = (type) => store.commit("sidebarType", type);

const sidebarColor = (color = "success") => {
  document.querySelector("#sidenav-main").setAttribute("data-color", color);
};

const darkMode = () => {
  if (store.state.darkMode) {
    store.state.darkMode = false;
    setSidebarType("bg-white");
    deactivateDarkMode();
    return;
  } else {
    store.state.darkMode = true;
    setSidebarType("bg-default");
    activateDarkMode();
  }
};
</script>
<template>
  <div class="fixed-plugin">
    <a
      class="px-3 py-2 fixed-plugin-button text-dark position-fixed"
      @click="toggleConfigurator"
    >
      <i class="py-2 fa fa-cog"></i>
    </a>
    <div class="shadow-lg card">
      <div class="pt-3 pb-0 bg-transparent card-header">
        <div class="" :class="isRTL ? 'float-end' : 'float-start'">
          <h5 class="mt-3 mb-0">Image Pipeline Theme</h5>
          <p>Change the theme options.</p>
        </div>
        <div
          class="mt-4"
          @click="toggleConfigurator"
          :class="isRTL ? 'float-start' : 'float-end'"
        >
          <button class="p-0 btn btn-link text-dark fixed-plugin-close-button">
            <i class="fa fa-close"></i>
          </button>
        </div>
        <!-- End Toggle Button -->
      </div>
      <hr class="my-1 horizontal dark" />
      <div class="pt-0 card-body pt-sm-3">
        <!-- Sidebar Backgrounds -->
        <div>
          <h6 class="mb-0">Sidebar Colors</h6>
        </div>
        <a href="#" class="switch-trigger background-color">
          <div
            class="my-2 badge-colors"
            :class="isRTL ? 'text-end' : ' text-start'"
          >
            <span
              class="badge filter bg-gradient-primary active"
              data-color="primary"
              @click="sidebarColor('primary')"
            ></span>
            <span
              class="badge filter bg-gradient-dark"
              data-color="dark"
              @click="sidebarColor('dark')"
            ></span>
            <span
              class="badge filter bg-gradient-info"
              data-color="info"
              @click="sidebarColor('info')"
            ></span>
            <span
              class="badge filter bg-gradient-success"
              data-color="success"
              @click="sidebarColor('success')"
            ></span>
            <span
              class="badge filter bg-gradient-warning"
              data-color="warning"
              @click="sidebarColor('warning')"
            ></span>
            <span
              class="badge filter bg-gradient-danger"
              data-color="danger"
              @click="sidebarColor('danger')"
            ></span>
          </div>
        </a>
        <!-- Navbar Fixed -->
        <!-- Navbar Fixed -->
        <div class="mt-3 d-flex">
          <h6 class="mb-0">Navbar Fixed</h6>
          <div class="form-check form-switch ps-0 ms-auto my-auto">
            <input
              class="mt-1 form-check-input"
              :class="isRTL ? 'float-end  me-auto' : ' ms-auto'"
              type="checkbox"
              id="navbarFixed"
              :checked="isNavFixed"
              @click="navbarFixed"
            />
          </div>
        </div>

        <hr class="horizontal dark my-4" />
        <div class="mt-2 mb-5 d-flex">
          <h6 class="mb-0" :class="isRTL ? 'ms-2' : ''">Light / Dark</h6>
          <div class="form-check form-switch ps-0 ms-auto my-auto">
            <input
              class="form-check-input mt-1 ms-auto"
              type="checkbox"
              :checked="store.state.darkMode"
              @click="darkMode"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
