<template>
    <v-container>
        <v-layout row justify="center">
            <v-flex>
                <v-card width=500px>
                    <v-card-text>
                        <v-container>
                            <v-card-title>Opret bruger</v-card-title>
                            <form @submit.prevent="onSignUp">
                                <v-layout row>
                                    <v-flex xs12>
                                        <v-text-field
                                        name="name"
                                        label="Navn"
                                        id="name"
                                        v-model="name"
                                        type="text"
                                        required> </v-text-field>
                                    </v-flex>
                                </v-layout>
                                <v-layout row>
                                    <v-flex xs12>
                                        <v-text-field
                                        name="email"
                                        label="E-Mail Adresse"
                                        id="email"
                                        v-model="email"
                                        type="email"
                                        required> </v-text-field>
                                    </v-flex>
                                </v-layout>
                                <v-layout row>
                                    <v-flex xs12>
                                        <v-text-field
                                        name="password"
                                        label="Password"
                                        id="password"
                                        v-model="password"
                                        type="password"
                                        required> </v-text-field>
                                    </v-flex>
                                </v-layout>
                                <v-layout row>
                                    <v-flex xs12>
                                        <v-text-field
                                        name="confirmPassword"
                                        label="Confirm Password"
                                        id="confirmPassword"
                                        v-model="confirmPassword"
                                        type="password"
                                        :rules=[comparePasswords]> </v-text-field>
                                    </v-flex>
                                </v-layout>
                                <v-layout row>
                                    <v-flex xs12>
                                     <v-card-actions>
                                        <v-btn type="Submit" color="primary">Opret</v-btn>
                                        <v-spacer></v-spacer>
                                        <v-btn @click="pressedClose">Luk</v-btn>
                                     </v-card-actions>
                                    </v-flex>
                                </v-layout>
                            </form>
                        </v-container>
                    </v-card-text>
                </v-card>
            </v-flex>
        </v-layout>
    </v-container>
</template>


<script>
import * as firebase from 'firebase/compat'
require('firebase/auth')
export default {
    name: "signup",
    data() {
        return {
            email: '',
            password: '',
            confirmPassword: ''
        }
    },
    computed: {
        comparePasswords() {
            return this.password !== this.confirmPassword ? 'Passwords do not match' : true
        }
    },
    methods: {
        pressedClose() {
            this.$emit('clicked', false)
        },
        onSignUp () {
            console.log(this.email)
            firebase.auth().createUserWithEmailAndPassword(this.email,this.password)
                .then(console.log("bruger oprettet"))
                .catch(error => console.log(error))
        }
    }

}
</script>
