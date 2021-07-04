<template>
  <div>
    <v-dialog persistent max-width="600" v-model="dialog">
      <v-card>
        <v-toolbar dense flat color="blue" dark>
          <v-toolbar-title>Item data </v-toolbar-title>
          <v-spacer></v-spacer>
          <v-btn color="white" text @click="cerrar">Cerrar</v-btn>
          <v-btn color="white" text @click="dialog2 = true">Agregar</v-btn>
        </v-toolbar>

        <v-col cols="12">
          <v-card
            v-for="(items, i) in data.items"
            :key="i"
            class="rounded-xl ma-6"
            elevation="19"
          >
            <v-container>
              <h2 class="mb-5">Data</h2>
              <v-row>
                <v-col cols="12" class="ma-0 pt-0 pb-0">
                  <v-text-field
                    outlined
                    color="green"
                    label="Name"
                    placeholder="Ingresa tu calle"
                    dense
                    v-model="items.name"
                    readonly
                  ></v-text-field>
                </v-col>
                <v-col cols="12" class="ma-0 pt-0 pb-0">
                  <v-text-field
                    outlined
                    color="green"
                    label="Price"
                    placeholder="Ingresa el número exterior"
                    type="number"
                    min="0"
                    max="99999"
                    dense
                    readonly
                    v-model="items.price"
                  ></v-text-field>
                </v-col>
                <v-col cols="12" class="ma-0 pt-0 pb-0">
                  <v-text-field
                    outlined
                    color="green"
                    label="Sku"
                    placeholder="Ingresa número interior"
                    type="text"
                    min="0"
                    max="99999"
                    dense
                    readonly
                    v-model="items.sku"
                  ></v-text-field>
                </v-col>
                <v-col cols="12" class="ma-0 pt-0 pb-0">
                  <v-text-field
                    outlined
                    color="green"
                    label="Quantity"
                    placeholder="Ingresa tu colonia"
                    dense
                    readonly
                    v-model="items.quantity"
                  ></v-text-field>
                </v-col>
              </v-row>
            </v-container>
          </v-card>
        </v-col>
      </v-card>
    </v-dialog>
    <v-dialog persistent max-width="600" v-model="dialog2">
      <v-card>
        <v-toolbar dense flat color="blue" dark>
          <v-toolbar-title>Item data </v-toolbar-title>
          <v-spacer></v-spacer>
        </v-toolbar>

        <v-col cols="12">
          <v-card class="rounded-xl ma-6" elevation="10">
            <v-container>
              <h2 class="mb-5">Data</h2>
              <v-row>
                <v-col cols="12" class="ma-0 pt-0 pb-0">
                  <v-text-field
                    outlined
                    color="green"
                    label="Name"
                    placeholder="Ingresa tu calle"
                    dense
                    v-model="name"
                  ></v-text-field>
                </v-col>
                <v-col cols="12" class="ma-0 pt-0 pb-0">
                  <v-text-field
                    outlined
                    color="green"
                    label="Price"
                    placeholder="Ingresa el número exterior"
                    type="number"
                    min="0"
                    max="99999"
                    dense
                    v-model="price"
                  ></v-text-field>
                </v-col>
                <v-col cols="12" class="ma-0 pt-0 pb-0">
                  <v-text-field
                    outlined
                    color="green"
                    label="Sku"
                    placeholder="Ingresa número interior"
                    type="text"
                    min="0"
                    max="99999"
                    dense
                    v-model="sku"
                  ></v-text-field>
                </v-col>
                <v-col cols="12" class="ma-0 pt-0 pb-0">
                  <v-text-field
                    outlined
                    color="green"
                    label="Quantity"
                    placeholder="Ingresa tu colonia"
                    dense
                    v-model="quantity"
                  ></v-text-field>
                </v-col>
              </v-row>
            </v-container>
            <v-card-actions class="pt-0">
              <v-spacer></v-spacer>
              <v-btn color="red" text @click="dialog2 = false">Cancelar</v-btn>
              <v-btn
                color="green darken-1"
                depressed
                class="white--text"
                @click="init"
                :loading="loading"
                >Guardar</v-btn
              >
            </v-card-actions>
          </v-card>
        </v-col>
      </v-card>
    </v-dialog>
    <v-overlay :value="loading">
      <v-progress-circular indeterminate size="64"></v-progress-circular>
    </v-overlay>
  </div>
</template>

<script>
export default {
  data() {
    return {
      loading: false,
      dialog2: false,
      name: "",
      price: "",
      sku: "",
      quantity: "",
      data: {},
    };
  },
  methods: {
    async init() {
      this.loading = true;
      await this.agregarItem();
      this.loading = false;
      this.dialog2 = false;
    },
    async agregarItem() {
      try {
        await this.data.items.push({
          name: this.name,
          price: this.price,
          sku: this.sku,
          quantity: this.quantity,
        });

        console.log("items de push", this.data.items);
      } catch (error) {
        console.log(error);
      } finally {
      }
    },
    cerrar() {
      this.dialog2 = false;
      this.$emit("cerrar");
    },
  },
  props: {
    dialog: {
      type: Boolean,
      required: true,
    },
    meta: {
      type: "",
      default: function () {
        return {};
      },
    },
  },
  watch: {
    meta: function () {
      this.data = Object.assign({}, this.meta);
    },
  },
};
</script>

<style lang="scss" scoped>
</style>