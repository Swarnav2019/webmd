<template>
    <v-app>
        <v-main>
            <v-container
                class="fill-height"
                fluid
            >
                <v-row
                    align="center"
                    justify="center"
                >
                    <v-col
                        cols="12"
                        sm="8"
                        md="4"
                    >
                        <v-form 
                            ref="form"
                            v-model="valid"
                            lazy-validation
                        >
                            <v-card class="login-form">
                                <v-toolbar
                                    align="center"
                                    light
                                    flat
                                >
                                    <v-toolbar-title>Member Login</v-toolbar-title>
                                </v-toolbar>
                                <v-card-text>
                                    <v-container>
                                        <v-row>
                                            <v-col cols="12">
                                                <text-box-component
                                                    v-model="form.email"
                                                    name="email"
                                                    :rules="emailRules"
                                                    @update-data="updateData"
                                                    icon="mdi-account"
                                                    type="text"
                                                    label="Username"
                                                />
                                            </v-col>

                                            <v-col cols="12">
                                                <text-box-component
                                                    v-model="form.password"
                                                    name="password"
                                                    :rules="passwordRules"
                                                    @update-data="updateData"
                                                    icon="mdi-lock"
                                                    type="password"
                                                    label="Password"
                                                />
                                            </v-col>

                                            <v-col cols="6">
                                                <check-box-component
                                                    v-model="form.remember"
                                                    label="Remember me"
                                                />
                                            </v-col>

                                            <v-col cols="6">
                                                <p class="forgot-password">
                                                    <router-link to="#"><i>Forgot Password?</i></router-link>
                                                </p>
                                            </v-col>

                                            <v-col cols="12">
                                                <v-btn 
                                                    :disabled="!valid"
                                                    color="#fb8c00"
                                                    x-large
                                                    @click="validate"
                                                >
                                                    Login
                                                </v-btn>
                                            </v-col>
                                        </v-row>
                                    </v-container>
                                </v-card-text>
                            </v-card>
                        </v-form>
                    </v-col>
                </v-row>
            </v-container>
        </v-main>
    </v-app>
</template>

<script>
const initialForm = {
    email: '',
    password: '',
    remember: true,
  };

import axios from 'axios'
import TextBoxComponent from './common/textBoxComponent'
import CheckBoxComponent from './common/checkBoxComponent'

export default {
  name: 'Login',

  components: {
      TextBoxComponent,
      CheckBoxComponent,
    },

  data () {
      return {
        valid: true,
        form: {
          ...initialForm
        },
        emailRules: [
            v => !!v || 'E-mail is required',
            v =>  /^[a-zA-Z0-9]+@[a-zA-Z0-9]+\.[a-z]{3}$/.test(v) || 'E-mail must be valid',
        ],
        passwordRules: [v => !!v || 'Password is required'],
      }
    },
  methods: {
      validate() {
        const isValid = this.$refs.form.validate();

        if(isValid) {
            axios
            .post(
                `https://jsonplaceholder.typicode.com/users`,
                this.form
            )
            .then(response => {
                console.log('Success', response.data)
            })
            .catch(error => {
                console.log('error', error)
            })
        }
      },

      updateData(data) {
          this.form = {...this.form, ...data};
      }
  }
}
</script>

<style>
    .v-toolbar__title {
        width: 100%;
    }

    .v-input {
        height: 52px;
    }

    .theme--light .v-label {
        color: #808080;
    }

    .theme--light .v-icon {
        color: #fb8c00 !important;
    }

    .forgot-password {
        position: relative;
        top: 23%;
        text-align: right;
        font-size: 16px;
    }

    .forgot-password a {
        text-decoration: none;
        color: #808080;
    }

    .v-btn__content {
        color: #FFFFFF;
    }
</style>