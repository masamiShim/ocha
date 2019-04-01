<template>
  <v-app
    dark
    id="inspire"
  >
    <v-navigation-drawer
      fixed
      clipped
      v-model="drawer"
      app
    >
      <v-list dense>
        <v-list-tile v-for="item in items" :key="item.text" @click="transPage(item.path)">
          <v-list-tile-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title>
              {{ item.text }}
            </v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
        <v-subheader class="mt-3 grey--text text--darken-1">SUBSCRIPTIONS</v-subheader>
        <v-list>
          <v-list-tile v-for="item in items2" :key="item.text" avatar @click="">
            <v-list-tile-avatar>
              <img :src="`https://randomuser.me/api/portraits/men/${item.picture}.jpg`" alt="">
            </v-list-tile-avatar>
            <v-list-tile-title v-text="item.text"></v-list-tile-title>
          </v-list-tile>
        </v-list>
        <v-list-tile class="mt-3" @click="">
          <v-list-tile-action>
            <v-icon color="grey darken-1">add_circle_outline</v-icon>
          </v-list-tile-action>
          <v-list-tile-title class="grey--text text--darken-1">Browse Channels</v-list-tile-title>
        </v-list-tile>
        <!-- // eslint-disable-next-line -->
        <v-list-tile @click="">
          <v-list-tile-action>
            <v-icon color="grey darken-1">settings</v-icon>
          </v-list-tile-action>
          <v-list-tile-title class="grey--text text--darken-1">Manage Subscriptions</v-list-tile-title>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
    <v-toolbar
      color="red"
      dense
      fixed
      clipped-left
      app
    >
      <v-toolbar-side-icon @click.stop="drawer = !drawer"></v-toolbar-side-icon>
      <v-icon class="mx-3">fa-youtube</v-icon>
      <v-toolbar-title class="mr-5 align-center">
        <span class="title">Youtube</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-layout row align-center style="max-width: 650px">
        <v-text-field
          placeholder="Search..."
          single-line
          append-icon="search"
          :append-icon-cb="() => {}"
          color="white"
          hide-details
        ></v-text-field>
      </v-layout>
    </v-toolbar>
    <v-content>
      <router-view />
    </v-content>
  </v-app>
</template>

<script>
  /* eslint-disable */
  import {
    VApp, VContent, VContainer, VFlex, VTooltip, VLayout, VBtn, VIcon, VTextField,
    VSpacer, VNavigationDrawer, VToolbar, VToolbarTitle, VToolbarSideIcon, VList,
    VListTile, VListGroup, VListTileAction, VListTileActionText, VListTileTitle, VListTileSubTitle,
    VListTileAvatar, VSubheader, VListTileContent
  } from 'vuetify/lib'

  export default {
    name: 'App',
    components: {
      VApp, VContent, VContainer, VFlex, VTooltip, VLayout, VBtn, VIcon,
      VTextField, VSpacer, VNavigationDrawer, VToolbar, VToolbarTitle, VToolbarSideIcon, VList,
      VListTile, VListGroup, VListTileAction, VListTileActionText, VListTileTitle, VListTileSubTitle,
      VListTileAvatar, VSubheader, VListTileContent
    },
    props: {
      source: String
    },
    data: () => ({
      drawer: true,
      items: [
        { icon: 'trending_up', text: 'Most Popular', path: '/' },
        { icon: 'subscriptions', text: 'Subscriptions', path: '/' },
        { icon: 'history', text: 'History', path: '/' },
        { icon: 'featured_play_list', text: 'Playlists', path: '/' },
        { icon: 'watch_later', text: 'Watch Later', path: '/' },
        { icon: 'edit', text: 'プロフィール編集', path: '/profile/edit' }
      ],
      items2: [
        { picture: 28, text: 'Joseph' },
        { picture: 38, text: 'Apple' },
        { picture: 48, text: 'Xbox Ahoy' },
        { picture: 58, text: 'Nokia' },
        { picture: 78, text: 'MKBHD' }
      ]
    }),
    methods: {
      transPage(path) {
        // TODO: これにuserIdみたいなんのっければ良さそう
        console.log(this.$router.currentRoute)
        if(this.$router.currentRoute.path === path){
          this.drawer = !this.drawer
          return
        }
        this.$router.push(path)
      }
    }
  }
</script>
