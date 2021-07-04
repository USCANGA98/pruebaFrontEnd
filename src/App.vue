<template>
  <v-app>
    <v-main class="blue darken-2">
      <v-navigation-drawer
        v-model="drawer"
        :mini-variant="miniVariant"
        :clipped="clipped"
        floating
        color="blue darken-2"
        permanent
        height="575"
        width="200"
        class="mt-10 ml-5 rounded-xl"
        app
      >
        <div class="d-flex mt-5 justify-center">
          <v-badge avatar bordered overlap>
            <template v-slot:badge>
              <v-avatar>
                <v-icon>mdi-check-decagram</v-icon>
              </v-avatar>
            </template>
            <v-hover v-slot:default="{ hover }">
              <v-avatar
                color="white"
                class="transition-swing"
                :class="`elevation-${hover ? 8 : 2}`"
                size="90"
              >
                <v-img
                  max-height="86"
                  max-width="86"
                  src="https://cdn.vuetifyjs.com/images/john.png"
                ></v-img>
              </v-avatar>
            </v-hover>
          </v-badge>
        </div>
        <p class="title text-center pt-3 white--text font-weight-black">
          Jhon Mircha
        </p>

        <!-- <v-card>
            <v-card color="blue" min-height="10" tile flat> </v-card>
            <v-list-item-content class="justify-center">
              <div class="mx-auto text-center">
                <v-hover v-slot:default="{ hover }" open-delay="0">
                  <v-btn class="mb-3 mt-3" depressed fab icon>
                    <v-avatar
                      :class="`elevation-${hover ? 4 : 1}`"
                      class="mb-2 mt-1 transition-swing"
                      color="white"
                      size="70"
                    >
                      <v-img
                        max-height="68"
                        max-width="68"
                        src="./assets/logo.png"
                      ></v-img>
                    </v-avatar>
                  </v-btn>
                </v-hover>
                <h3>
                  Administrador
                  <v-icon color="blue" small> mdi mdi-check-decagram</v-icon>
                </h3>
                <p class="caption mt-1">Administrador</p>
              </div>
            </v-list-item-content>
          </v-card> -->

        <v-list dense rounded class="mx-n1">
          <v-list-item v-for="item in items" :key="item.title" link exact>
            <v-list-item-icon>
              <v-icon color="white">{{ item.icon }}</v-icon>
            </v-list-item-icon>
            <v-list-item-content>
              <v-list-item-title
                class="white--text font-weight-light"
                v-text="item.title"
              />
            </v-list-item-content>
          </v-list-item>
        </v-list>
        <div class="subtitle-2 font-weight-light white--text mx-4">
          insights
        </div>
        <v-list dense rounded class="mx-n1">
          <v-list-item link>
            <v-list-item-icon>
              <v-icon color="white">mdi-mail</v-icon>
            </v-list-item-icon>
            <v-list-item-content>
              <v-list-item-title class="font-weight-light white--text"
                >Messages</v-list-item-title
              >
            </v-list-item-content>

            <v-list-item-avatar
              color="red"
              size="20"
              class="white--text justify-center"
            >
              1
            </v-list-item-avatar>
          </v-list-item>
          <v-list-item link>
            <v-list-item-icon>
              <v-icon color="white">mdi-bell</v-icon>
            </v-list-item-icon>
            <v-list-item-content>
              <v-list-item-title class="font-weight-light white--text">
                Notifications
              </v-list-item-title></v-list-item-content
            >

            <v-list-item-avatar
              size="20"
              color="red"
              class="white--text justify-center"
            >
              6
            </v-list-item-avatar>
          </v-list-item>
        </v-list>
        <template v-slot:append>
          <div>
            <v-btn
              block
              color="white"
              class="font-weight-medium text-capitalize"
            >
              <v-icon color="red" left>mdi-account-arrow-left</v-icon> Cerrar
              sesión
            </v-btn>
          </div>
        </template>
      </v-navigation-drawer>
      <v-app-bar
        class="pl-3 rounded-xl"
        color="blue darken-2"
        elevation="0"
        fixed
        height="60"
        app
      >
        <v-btn
          active-class="yellow white--text"
          v-for="(item, i) in items"
          :key="i"
          text
          class="white--text pa-3 text-capitalize font-weight-light rounded-xl"
          ><v-icon left>{{ item.icon }}</v-icon>
          {{ item.title }}
        </v-btn>
        <v-spacer></v-spacer>
        <v-btn icon>
          <v-icon color="white"> mdi-bell </v-icon>
        </v-btn>
        <v-btn icon>
          <v-icon color="white"> mdi-chat-processing </v-icon>
        </v-btn>
        <v-btn icon>
          <v-avatar size="24">
            <v-img src="https://cdn.vuetifyjs.com/images/john.png"></v-img>
          </v-avatar>
        </v-btn>
        <v-app-bar-nav-icon color="white" @click.stop="drawer = !drawer" />

        <v-menu max-width="250" transition="no" bottom min-width="200" offset-x>
          <template v-slot:activator="{ on: menu }">
            <v-btn icon small v-on="{ ...menu }">
              <v-icon color="white">mdi-chevron-down</v-icon>
            </v-btn>
          </template>

          <v-card>
            <v-card color="blue" min-height="10" tile flat> </v-card>
            <v-card-title>Configuracion</v-card-title>
            <v-list-item-content class="justify-center">
              <div class="mx-auto text-center">
                <v-divider class="my-3"></v-divider>
                <v-btn depressed rounded text> Cerrar Sesión </v-btn>
              </div>
            </v-list-item-content>
          </v-card>
        </v-menu>
        <!-- <v-btn icon @click.stop="rightDrawer = !rightDrawer">
        <v-icon>mdi-menu</v-icon>
      </v-btn> -->
      </v-app-bar>

      <HelloWorld />
    </v-main>
  </v-app>
</template>

<script>
import HelloWorld from "./components/HelloWorld";

export default {
  name: "App",

  components: {
    HelloWorld,
  },

  data: () => ({
    clipped: false,
    drawer: false,
    fixed: false,
    items: [
      {
        icon: "mdi-view-dashboard",
        title: "Inicio",
      },
      {
        icon: "mdi-clock-fast",
        title: "Hoy",
      },
      {
        icon: "mdi-account-multiple-check",
        title: "Siguiendo",
      },
    ],

    miniVariant: false,
    right: true,
    rightDrawer: false,
    title: "Vuetify.js",
  }),
};
</script>

