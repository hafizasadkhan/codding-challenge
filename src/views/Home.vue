<template>
  <v-app id="inspire">
    <v-navigation-drawer
            v-model="drawer"
            app
            clipped
    >
      <v-list dense shaped>
        <v-list-item-group v-model="item" color="primary">
          <v-list-item
                  v-for="(item, i) in items"
                  :key="i"
                  :to="item.to"
                  exact
          >
            <v-list-item-icon>
              <v-icon v-text="item.icon"></v-icon>
            </v-list-item-icon>
            <v-list-item-content>
              <v-list-item-title v-text="item.text"></v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </v-list-item-group>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar
            app
            clipped-left
    >
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-toolbar-title>Artist Finder</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-switch
              v-model="$vuetify.theme.dark"
              hide-details
              class="mx-3"
              inset
              label="Theme Dark"/>
    </v-app-bar>

    <v-content>
      <v-container
              fluid
      >
        <router-view/>
      </v-container>
    </v-content>

    <v-footer app>
      <span>&copy; 2019</span>
    </v-footer>
  </v-app>
</template>

<script>
  export default {
    props: {
      source: String,
    },
    data: () => ({
      drawer: null,
      item: 1,
      items: [
        { text: 'Search Artist', icon: 'mdi-face',to:'/home' },
        { text: 'About', icon: 'info',to:'/home/about' },
      ],
    }),
    created () {
    },
  }
</script>
