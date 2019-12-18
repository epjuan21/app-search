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
          <v-card class="mx-auto" outlined>
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
          </v-card>
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
        console.log(this.items)
        this.loading = false;
      });
    }, 500),

    clearQuery() {
      this.query = null
      this.items = []
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
