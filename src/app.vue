<template>
  <v-app>
    <v-toolbar app tabs>
      <v-toolbar-title>
        <h1 class="display-1">@scriptdaemon</h1>
      </v-toolbar-title>
      <v-tabs slot="extension" grow>
        <v-tab :to="{ name: 'page1' }">Page 1</v-tab>
        <v-tab :to="{ name: 'page2' }">Page 2</v-tab>
        <v-tab :to="{ name: 'page3' }">Page 3</v-tab>
      </v-tabs>
    </v-toolbar>
    <v-content>
      <v-container>
        <transition :name="transition" mode="out-in">
          <router-view/>
        </transition>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      transition: 'slide-left'
    }
  },
  watch: {
    $route (to, from) {
      this.transition = to.meta.index < from.meta.index
        ? 'slide-right'
        : 'slide-left'
    }
  }
}
</script>

<style>
@import '~vuetify/dist/vuetify.min.css';

.slide-right-enter-active,
.slide-left-enter-active {
  transition: 250ms ease-out;
}

.slide-right-leave-active,
.slide-left-leave-active {
  transition: 250ms ease-in;
}

.slide-right-enter,
.slide-right-leave-to,
.slide-left-enter,
.slide-left-leave-to {
  opacity: 0;
}

.slide-right-enter,
.slide-left-leave-to {
  transform: translate(-100%, 0);
}

.slide-right-leave-to,
.slide-left-enter {
  transform: translate(100%, 0);
}
</style>
