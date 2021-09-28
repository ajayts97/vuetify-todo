<template>
  <v-app id="inspire">
    <v-navigation-drawer v-model="drawer" app mobile-breakpoint="768">
      <v-img
        class="pa-4"
        src="https://images.unsplash.com/photo-1621789098776-ced8d56901b4"
        gradient="to top right, rgba(19,84,122,.5), rgba(128,208,199,.8)"
        height="170"
      >
        <v-avatar size="70" class="pt-2">
          <img src="@/assets/images/myavatar.jpg" alt="Ajay" />
        </v-avatar>
        <div class="white--text text-subtitle-1 font-weight-bold pt-1">
          AJAY T S
        </div>
        <div class="white--text text-subtitle-2">ajay_ts</div>
      </v-img>

      <v-list dense nav>
        <v-list-item v-for="item in items" :key="item.title" :to="item.to" link>
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar
      app
      color="primary"
      dark
      src="https://images.unsplash.com/photo-1621789098776-ced8d56901b4"
      prominent
      :height="$route.path === '/' ? '238' : '170'"
    >
      <template v-slot:img="{ props }">
        <v-img
          v-bind="props"
          gradient="to top right, rgba(19,84,122,.9), rgba(128,208,199,.9)"
        ></v-img>
      </template>
      <v-container class="header-container pa-0 mt-2">
        <v-row>
          <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
          <v-spacer></v-spacer>
          <search />
        </v-row>
        <v-row>
          <v-app-bar-title class="ttext-h4 ml-4">{{
            $store.state.appTitle
          }}</v-app-bar-title>
        </v-row>
        <v-row>
          <live-date-time />
        </v-row>
        <v-row v-if="$route.path === '/'">
          <field-add-task />
        </v-row>
      </v-container>
    </v-app-bar>

    <v-main>
      <router-view></router-view>
      <snackbar />
    </v-main>
  </v-app>
</template>

<script>
export default {
  data: () => ({
    drawer: null,
    items: [
      { title: 'Todo', icon: 'mdi-format-list-checks', to: '/' },
      { title: 'About', icon: 'mdi-help-box', to: '/about' },
    ],
  }),
  // computed: {
  //   appTitle() {
  //     return process.env.VUE_APP_TITLE;
  //   },
  // },
  mounted() {
    this.$store.dispatch('getTasks');
  },

  components: {
    snackbar: require('@/components/Shared/Snackbar.vue').default,
    search: require('@/components/Tools/Search.vue').default,
    'live-date-time': require('@/components/Tools/LiveDateTime.vue').default,
    'field-add-task': require('@/components/Todo/FieldAddTask.vue').default,
  },
};
</script>
<style lang="sass">
.header-container
  max-width : none !important
</style>
