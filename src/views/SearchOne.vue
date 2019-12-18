<template>
  <div>
    <v-container>
      <v-row>
        <v-col>
          <h1 class="font-weight-light title">Buscador Códigos Invima</h1>
        </v-col>
      </v-row>
      <v-row>
        <v-col>
          <v-card>
            <v-card-title>
              <v-text-field
                prepend-icon="mdi-magnify"
                :clearable="clearable"
                :loading="loading"
                hint="Digite el nombre del producto o el registro INVIMA"
                persistent-hint
                label="Buscar"
                v-model="query"
                @click:clear="clearQuery()"
              >
              </v-text-field>
            </v-card-title>
            <v-divider></v-divider>
            <v-card-text class="py-1 ml-8">
              Resultados: {{ itemsLength }}
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
      <div></div>

      <v-row v-if="isData">
        <v-col cols="12">
          <!-- <v-card class="mx-auto" outlined>
            <v-card-text>
              <v-simple-table>
                <template v-slot:default>
                  <thead>
                    <tr>
                      <th class="text-left">Nombre</th>
                      <th class="text-left">Código CUM</th>
                      <th class="text-left">Registro Invima</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="item in items">
                      <td>{{ item.producto }}</td>
                      <td>
                        {{ item.expedientecum }}-{{ item.consecutivocum }}
                      </td>
                      <td>{{ item.registrosanitario }}</td>
                    </tr>
                  </tbody>
                </template>
              </v-simple-table>
            </v-card-text>
          </v-card> -->

          <div class="box-wrapper margin-bottom" v-for="item in items">
            <div class="box-header">
              <div class="item-wrapper">
                <div class="item-value-header">
                  {{ item.producto }}
                </div>
                <div class="item-key-header">Producto</div>
              </div>
              <div class="icon-wrapper">
                <div class="icon-box">
                  <div v-if="item.estadoregistro == 'Vigente'">
                    <v-icon color="teal lighten-2">mdi-check-circle</v-icon>
                  </div>
                  <div v-else>
                    <v-icon color="red">mdi-close-circle</v-icon>
                  </div>
                  <span>Registro</span>
                </div>
                <div class="icon-box">
                  <div v-if="item.estadocum == 'Activo'">
                    <v-icon color="teal lighten-2">mdi-check-circle</v-icon>
                  </div>
                  <div v-else>
                    <v-icon color="red">mdi-close-circle</v-icon>
                  </div>
                  <span>CUM</span>
                </div>
              </div>
            </div>

            <div class="row-space-between">
              <div class="item-wrapper">
                <div class="item-value">
                  {{ item.descripcioncomercial }}
                </div>
                <div class="item-key">Descripción Comercial</div>
              </div>
            </div>

            <div class="row-space-start">
              <div class="item-wrapper">
                <div class="item-value">{{ item.principioactivo }}</div>
                <div class="item-key">Principio Activo</div>
              </div>
              <div class="item-wrapper">
                <div class="item-value">{{ item.atc }}</div>
                <div class="item-key">ATC</div>
              </div>
              <div class="item-wrapper">
                <div class="item-value">{{ item.descripcionatc }}</div>
                <div class="item-key">Descripción ATC</div>
              </div>
              <div class="item-wrapper">
                <div class="item-value">{{ item.expedientecum }}-{{ item.consecutivocum }} </div>
                <div class="item-key">CUM</div>
              </div>
              <div class="item-wrapper">
                <div class="item-value">{{ item.registrosanitario }}</div>
                <div class="item-key">Registro Sanitario</div>
              </div>
            </div>

            <div class="row-space-start margin-bottom">
              <div class="item-wrapper">
                <div class="item-value">{{ item.muestramedica }}</div>
                <div class="item-key">Muestra Médica</div>
              </div>

              <div class="item-wrapper">
                <div class="item-value">{{ item.unidad }}</div>
                <div class="item-key">Unidad</div>
              </div>

              <div class="item-wrapper">
                <div class="item-value">{{ item.unidadmedida }}</div>
                <div class="item-key">Unidad de Medida</div>
              </div>

              <div class="item-wrapper">
                <div class="item-value">{{ item.cantidad }}</div>
                <div class="item-key">Cantidad</div>
              </div>

              <div class="item-wrapper">
                <div class="item-value">{{ item.unidadreferencia }}</div>
                <div class="item-key">Unidad de Referencia</div>
              </div>

              <div class="item-wrapper">
                <div class="item-value">{{ item.formafarmaceutica }}</div>
                <div class="item-key">Forma Farmaceutica</div>
              </div>

              <div class="item-wrapper">
                <div class="item-value">{{ item.vidaadministracion }}</div>
                <div class="item-key">Via Administración</div>
              </div>
            </div>

            <div class="box-footer">
              <div class="icon-wrapper">
                <div class="icon-box-footer">
                  <i class="fas fa-city color-lightseagreen"></i>
                </div>
              </div>
              <div class="row-space-end">
                <div class="item-wrapper">
                  <div class="item-value">
                    {{ item.titular }}
                  </div>
                  <div class="item-key">Titular</div>
                </div>
                <div class="item-wrapper">
                  <div class="item-value">
                    {{ item.nombrerol }}
                  </div>
                  <div class="item-key">Nombre Rol</div>
                </div>
              </div>
            </div>
          </div>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import _ from "lodash";
export default {
  name: "SearchOne",
  data() {
    return {
      items: [],
      query: null,
      url: "",
      clearable: true,
      loading: false
    };
  },

  computed: {
    setQueryToUppercase() {
      if (this.query) {
        return this.query.toUpperCase();
      } else {
        return this.query;
      }
    },

    // baseUrl() {
    //   return (this.url = `https://www.datos.gov.co/resource/i7cb-raxc.json?$where=producto like '%25${this.setQueryToUppercase}%25' OR registrosanitario like '%25${this.setQueryToUppercase}%25'`);
    // },

    itemsLength() {
      if (this.items) {
        return this.items.length;
      } else {
        return 0;
      }
    },
    isData() {
      if (this.items == null || this.items == "") {
        return false;
      } else {
        return true;
      }
    }
  },
  watch: {
    query() {
      this.isQueryEmpty();
    }
  },

  methods: {
    searchAfterDebounce: _.debounce(function() {
      this.search();
    }, 500),

    search: _.debounce(function() {
      this.loading = true;
      this.url = `https://www.datos.gov.co/resource/i7cb-raxc.json?$where=producto like '%25${this.setQueryToUppercase}%25' OR registrosanitario like '%25${this.setQueryToUppercase}%25'`;
      this.$http.get(this.url).then(response => {
        this.items = response.data;
        console.log(this.items);
        this.loading = false;
      });
    }, 500),

    clearQuery() {
      this.query = null;
      this.items = [];
    },

    isQueryEmpty() {
      if (this.query === "") {
        this.items = [];
      } else {
        this.search();
      }
    }
  }
};
</script>
<style scoped>
@import url("https://fonts.googleapis.com/css?family=Open+Sans+Condensed:700|Roboto:300,400,700&display=swap");

.color-green {
  color: #5c940d;
}

.color-red {
  color: #c92a2a;
}

.color-lightseagreen {
  color: lightseagreen;
}

.margin-bottom {
  margin-bottom: 5px;
}

.row-space-between {
  display: flex;
  justify-content: space-between;
}

.row-space-end {
  display: flex;
  justify-content: flex-end;
}

.row-space-start {
  display: flex;
  justify-content: flex-start;
  flex-wrap: wrap;
}

.box-wrapper {
  width: auto;
  min-width: 600px;
  border: 1px solid rgba(0, 0, 0, 0.12);
  border-left: 3px solid blueviolet;
  border-radius: 4px;
  background-color: ghostwhite;
  padding: 0px 5px;
}

.box-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-bottom: 5px;
  padding-right: 5px;
  border-bottom: 1px solid lightseagreen;
}

.box-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-top: 1px solid lightseagreen;
  padding-bottom: 5px;
}

.icon-wrapper {
  display: flex;
}

.icon-box,
.icon-box-footer {
  display: flex;
  align-items: center;
}

.icon-box span {
  font-size: 12px;
  color: #adb5bd;
  margin-left: 5px;
  line-height: 12px;
}

.icon-wrapper .icon-box:last-child {
  margin-left: 12px;
}

.icon-wrapper .icon-box-footer {
  margin-left: 10px;
}

.item-wrapper {
  margin-top: 5px;
  display: inline-block;
  padding: 5px;
  margin-right: 5px;
}

.item-value-header {
  font-size: 15px;
  font-family: "Open Sans Condensed", sans-serif;
  font-weight: 700;
  color: #17202a;
}

.item-value {
  font-size: 12px;
  color: #17202a;
  margin-bottom: 2px;
}

.item-key-header {
  font-size: 12px;
  color: #495057;
}

.item-key {
  font-size: 11px;
  color: #868e96;
}
</style>
