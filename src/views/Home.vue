<template>
  <v-container>
    <v-row>
      <v-col>
        <h1 class="font-weight-light title">Inicio</h1>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <v-card class="mx-auto" max-width="400">
          <v-img
            class="black--text align-end"
            height="200px"
            src="https://cdn.pixabay.com/photo/2016/12/05/19/43/pill-1884775_960_720.jpg"
          >
            <v-card-title>Buscador Registros Vigentes</v-card-title>
          </v-img>

          <v-card-subtitle class="pb-0">Registros de Medicamentos Vigentes</v-card-subtitle>

          <v-card-text class="text--primary">
            <div>Buscador de Códigos CUM</div>

            <div>Se puede buscar por nombre del medicamento y por registro sanitario INVIMA</div>
          </v-card-text>

          <v-card-actions>
            <v-btn color="orange" text to="search-one">
              Ir al buscador
            </v-btn>

          </v-card-actions>
        </v-card>
      </v-col>
      <v-col>
        <v-card class="mx-auto" max-width="400">
          <v-img
            class="black--text align-end"
            height="200px"
            src="https://cdn.pixabay.com/photo/2016/12/05/19/43/pill-1884775_960_720.jpg"
          >
            <v-card-title>Buscador Registros Vencidos</v-card-title>
          </v-img>

          <v-card-subtitle class="pb-0">Registros de Medicamentos Vencidos</v-card-subtitle>

          <v-card-text class="text--primary">
            <div>Buscador de Códigos CUM</div>

            <div>Se puede buscar por nombre del medicamento y por registro sanitario INVIMA</div>
          </v-card-text>

          <v-card-actions>
            <v-btn color="orange" text to="search-two">
              Ir al buscador
            </v-btn>

          </v-card-actions>
        </v-card>        
      </v-col>

    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "home"
};
</script>
