<template>
  <div class="card text-center m-3">
    <h5 class="card-header">Crear Usuario</h5>
      <div class="card-body">   
        <v-form v-model="valid">
          <v-container>
            <v-row>
              <v-col cols="12" md="4">
                <v-text-field v-model="firstname" :rules="nameRules"  :counter="10" label="Name"  required ></v-text-field>
              </v-col>
              <v-col  cols="12" md="4">
                <select v-model="selected">
                  <option>male</option>
                  <option>female</option>
                </select>
                <span>Genero: {{ selected }}</span>
                <select v-model="selectedes">
                  <option>Acitvo</option>
                  <option>Inactivo</option>
                </select>
                <span>Estadus: {{ selectedes }}</span>
              </v-col>
              <v-col cols="12" md="4">
                <v-text-field v-model="email" :rules="emailRules" label="E-mail" required ></v-text-field>
              </v-col>
            </v-row>
        </v-container>
      </v-form>
      <v-btn @click="created" depressed color="blue darken-2">
        <v-icon class="mr-1">
            mdi-account-plus
        </v-icon>
      </v-btn>
    </div>
  </div>

</template>

<script>
import axios from 'axios';

export default {
   name: "create-user",
      data: () => ({
      totalVuePackages: null,
      name: '',
      phoneNumber: '',
      email: '',
      select: null,
    }),
       methods: {
          setActiveTab(){
              let _this = this;
              _this.activeTab = 1;
          },

            
  async created() {
          const headers = {
          "Content-Type": "application/json" ,
          "Authorization": "Bearer 46c804c946208176e0874b5b36132591d39891ec000375e208297c75ddd09079"
          };
          var data ={
              name: "Yo",
              gender: "male",
              email: "teiyokkk.@15ce.com",
              status: "active"
          }

          const response = await axios.post("https://gorest.co.in/public/v1/users", data,{ headers });
          this.totalVuePackages = response.data.total;
          }
      }
};
</script>


