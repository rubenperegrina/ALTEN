<template>
  <v-app>
    <template>
      <v-stepper v-model="e1">
        <v-stepper-header>
          <v-stepper-step :complete="e1 > 1" step="1">Name</v-stepper-step>

          <v-divider></v-divider>

          <v-stepper-step :complete="e1 > 2" step="2">Age</v-stepper-step>

          <v-divider></v-divider>

          <v-stepper-step step="3">Send</v-stepper-step>
        </v-stepper-header>

        <v-stepper-items>
          <v-stepper-content step="1">
            <p class="text-xs-center">Wellcome</p>
            <v-flex xs12 sm6 md3>
              <v-text-field v-model="person.name" label="What`s your name?"></v-text-field>
            </v-flex>
            <v-flex class="text-xs-center">
              <v-btn
                color="success"
                :disabled="!person.name || person.name == '' "
                @click="e1 = 2"
                center
              >Next</v-btn>
            </v-flex>
          </v-stepper-content>

          <v-stepper-content step="2">
            <v-text-field v-model="person.age" label="How old are you?"></v-text-field>

            <v-flex class="text-xs-center">
              <v-btn
                color="success"
                :disabled="!person.age || person.age <= 0 "
                @click="e1 = 3"
              >Next</v-btn>

              <v-btn color="secondary" @click="e1 = 1">Back</v-btn>
            </v-flex>
          </v-stepper-content>

          <v-stepper-content step="3">
            <p class="text-xs-center">Resume</p>

            <ul>
              <li v-for="(newUser, index) in person" :key="index">{{ newUser }}</li>
            </ul>
            <v-flex class="text-xs-center">
              <v-btn color="success" @click="sendData">Send</v-btn>
            </v-flex>
          </v-stepper-content>
        </v-stepper-items>
      </v-stepper>
    </template>
  </v-app>
</template>

<script>
import axios from "axios";
export default {
  name: "Form",
  data() {
    return {
      e1: 0,
      person: {
        name: "",
        age: undefined
      }
    };
  },
  methods: {
    sendData() {
      axios({
        method: "POST",
        url: "https://myApi.org/post",
        data: this.person,
        headers: { "content-type": "application/json" }
      }).then(
        result => {
          //     // Success
          //     this.e1 = 1;
          //     this.person.name = "";
          //     this.person.age = 0;
          //alert(result.data)
        },
        error => {
          //     // Error
          //alert(result.data)
        }
      );
    }
  }
};
</script>

<style>
</style>

