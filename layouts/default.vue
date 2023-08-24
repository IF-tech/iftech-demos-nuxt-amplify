<template>
  <v-app dark>
    <v-navigation-drawer
      mobile-breakpoint="580"
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      location="bottom"
      temporary
      app
    >
      <v-list>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar :clipped-left="clipped" fixed app>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <!-- <v-btn
        icon
        @click.stop="miniVariant = !miniVariant"
      >
        <v-icon>mdi-{{ `chevron-${miniVariant ? 'right' : 'left'}` }}</v-icon>
      </v-btn> -->
      <!-- <v-btn
        icon
        @click.stop="clipped = !clipped"
      >
        <v-icon>mdi-application</v-icon>
      </v-btn> -->
      <v-spacer />
      <v-toolbar-title v-text="title" />
      <v-spacer />
    </v-app-bar>
    <v-main>
      <Nuxt />
    </v-main>
    <v-footer fixed app>
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      clipped: null,
      drawer: false,
      fixed: null,
      items: [
        {
          icon: 'mdi-heart',
          title: 'Welcome',
          to: '/',
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'My Toolset',
          to: '/inspire',
        },
        {
          icon: 'mdi-fire',
          title: 'Campfire Scene',
          to: '/campfirescene',
        },
        {
          icon: 'mdi-atom',
          title: 'Taurus Knot',
          to: '/taurusknot',
        },
      ],
      miniVariant: null,
      title: 'Ian Floyd Technology',
    }
  },
}
</script>
