<template>
  <v-container class="pr-10 pl-10">
    <v-container> </v-container>
    <v-card class="ma-5" rounded="xl">
      <v-card-title>
        Items

        <v-menu
          max-width="250"
          transition="scale-transition"
          bottom
          :close-on-content-click="false"
          min-width="200"
          offset-x
        >
          <template v-slot:activator="{ on: menu, attrs }">
            <v-tooltip color="grey darken-3" bottom>
              <template v-slot:activator="{ on: tooltip }">
                <v-btn
                  @click="notification = false"
                  class="mx-1"
                  v-bind="attrs"
                  v-on="{ ...tooltip, ...menu }"
                  icon
                >
                  <v-badge
                    :content="notification"
                    :value="notification"
                    color="error"
                    overlap
                    dot
                    right
                  >
                    <v-icon :class="notification ? 'shake' : ''">
                      mdi-bell
                    </v-icon>
                  </v-badge>
                </v-btn>
              </template>
              <span>Orden de pedidos</span>
            </v-tooltip>
          </template>
          <v-card>
            <v-card-title>Lista de pedidos</v-card-title>
            <v-divider></v-divider>
            <v-list-item
              style="color: grey"
              class="subtitle-2"
              v-for="data in data.orders"
              :key="data.number"
            >
              {{ data.number }} -
              <span v-for="(item, index) in data.items" :key="index"
                >{{ item.name }}
                <v-icon color="green"
                  >mdi-checkbox-multiple-marked-circle-outline</v-icon
                >
              </span>
            </v-list-item>
          </v-card>
        </v-menu>

        <v-spacer></v-spacer>
        <v-text-field
          v-model="search"
          append-icon="mdi-magnify"
          label="Search"
          single-line
          hide-details
        ></v-text-field>
      </v-card-title>
      <v-data-table
        class="ma-3"
        :headers="headers"
        :items="items"
        :search="search"
      >
        <template v-slot:item.acciones="{ item }">
          <v-btn icon dark color="blue" @click="verUsuario(item)"
            ><v-icon> mdi-file-document-multiple </v-icon></v-btn
          >
        </template>
      </v-data-table>
    </v-card>

    <Dialog :meta="meta" @cerrar="dialog = false" :dialog="dialog" />
  </v-container>
</template>

<script>
import axios from "axios";
import Dialog from "./Dialog.vue";
export default {
  name: "HelloWorld",
  components: {
    Dialog,
  },
  data: () => ({
    notification: true,
    search: "",
    dialog: false,
    data: [],
    meta: [],
    items: [],
    headers: [
      {
        text: "Id",
        value: "id",
      },
      {
        text: "Number",
        value: "number",
      },
      {
        text: "Orden",
        value: "name",
      },
      {
        text: "Acciones",
        value: "acciones",
      },
    ],
  }),
  async mounted() {
    await this.getData();
  },
  methods: {
    verUsuario(meta) {
      this.meta = Object.assign({}, meta);
      this.dialog = true;
    },
    async getData() {
      try {
        const headers = {
          Authorization: `eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJwUGFINU55VXRxTUkzMDZtajdZVHdHV3JIZE81cWxmaCIsImlhdCI6MTYyMDY2Mjk4NjIwM30.lhfzSXW9_TC67SdDKyDbMOYiYsKuSk6bG6XDE1wz2OL4Tq0Og9NbLMhb0LUtmrgzfWiTrqAFfnPldd8QzWvgVQ`,
        };

        const { data } = await axios.get(
          `https://eshop-deve.herokuapp.com/api/v2/orders`,
          { headers }
        );
        if (data.success) {
          data.orders.forEach((e) => {
            this.items.push(e);
          });
          data.orders.forEach((e) => {
            this.meta.push(e.items[0]);
          });
        }
        this.data = data;
        // console.log(data);
      } catch (error) {
        console.warn(error);
      }
    },
  },
};
</script>
<style lang="scss">
.shake {
  animation: shake 2s ease infinite;
}
@keyframes shake {
  5% {
    transform: rotate(10deg);
  }
  10% {
    transform: rotate(-10deg);
  }
  15% {
    transform: rotate(10deg);
  }
  20% {
    transform: rotate(-10deg);
  }
  30% {
    transform: rotate(0deg);
  }
}
</style>
