<template>
    <v-container class="grey lighten-5">
        <h5  class="card-header text-center">Listas de Usuarios</h5>
    <v-row no-gutters>
      <v-col v-for="user in usuarios" :key="user" cols="12" sm="4">
      <v-card class="mx-auto" color="#26c6da" dark max-width="500">
      <div>
        <v-card-title>
            <v-icon large left>
                {{user.name}}
            </v-icon>
            <span class="text-h6 font-weight-light"> {{ user.id}}</span>
        </v-card-title>

        <v-card-text class="text-h5 font-weight-bold">
            {{ user.email}}
        </v-card-text>

        <v-card-actions>
            <v-list-item class="grow">
                <v-list-item-content>
                    <v-list-item-title>{{ user.gender}}</v-list-item-title>
                </v-list-item-content>

                <v-row align="center" justify="end">
                    <v-icon @click="edit(user.id, $event)" class="mr-1">
                        mdi-account-edit
                    </v-icon>

                    <v-icon @click="deletes(user.id, $event)" depressed  class="mr-1">
                        mdi-delete
                    </v-icon>
                    <v-spacer></v-spacer>
                
                    <v-btn icon @click="show = !show">
                        <v-icon>{{ show ? 'mdi-chevron-up' : 'mdi-chevron-down' }}</v-icon>
                    </v-btn>
                </v-row>

            </v-list-item>
        </v-card-actions>
      </div>

            <v-expand-transition>
                <div v-show=" user.id == ver">
                    <v-divider></v-divider>
                    <v-form  v-model="valid">
                        <v-container class="input-text" >
                            <v-row>
                                <v-col cols="12" md="4">
                                    <v-text-field v-model="firstname" :rules="nameRules" :counter="10" label="Name" required></v-text-field>
                                </v-col>
                                <v-col cols="12" md="4">
                                    <select v-model="selected">
                                        <option>male</option>
                                        <option>female</option>
                                    </select>
                                    <span>Genero: {{ selected }}</span>
                                    <select v-model="selectedes">
                                        <option>Acitvo</option>
                                        <option>Inactivo</option>
                                    </select>
                                    <span>Estatus: {{ selectedes }}</span>
                                </v-col>
                                <v-col cols="12" md="4">
                                    <v-text-field v-model="email" :rules="emailRules" label="E-mail" required ></v-text-field>
                                </v-col>
                            </v-row>
                        </v-container>
                    </v-form>
                </div>
            </v-expand-transition>
         </v-card>
      </v-col>
    </v-row>
    </v-container>
</template>

<script>

import axios from 'axios';

export default {
  name: "get-user",
  data() {
    return {
        show: false,
        usuarios: null,
        ver: Number,
    };
  },
    methods: {
        
            deletes(id) {
                const headers = { 
                    "Content-Type": "application/json",
                    "Accept" :"application/json",
                    "Authorization": "Bearer 46c804c946208176e0874b5b36132591d39891ec000375e208297c75ddd09079"
                    };
                        axios.delete("https://gorest.co.in/public/v1/users/"+id , {headers, id})
                            .then(response =>{
                                    console.log(response)
                                    this.reloadPage()
                                    }
                                );
                } ,
                reloadPage() {
                    window.location.reload();
                },

                async edit(id) {


                        const headers = {
          "Content-Type": "application/json" ,
          "Authorization": "Bearer 46c804c946208176e0874b5b36132591d39891ec000375e208297c75ddd09079"
          };
          var data ={
              name: "test",
              gender: "male",
              email: "t.@15ce.com",
              status: "active"
          }

                    this.ver = id;

          const response = await axios.patch(`https://gorest.co.in/public/v1/users/${id}`, data,{ headers });
          this.totalVuePackages = response.data.total;
          }
        },
            // funcion async await , nota: solo es para ver las diferentes formas que existe de desarrollo
            async created() {
                const response = await axios.get("https://gorest.co.in/public/v1/users?page=30");
                this.usuarios = response.data.data;
            }
    };
</script>

<style scoped lang="scss">
    .input-text {
        ::v-deep {
            .v-text-field {
                input {
                    color: blue;
                }
            }
        }
    }
</style>