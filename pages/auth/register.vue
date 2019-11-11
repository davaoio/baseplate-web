<template>
  <div>
    <v-content>
      <v-container class="fill-height" fluid>
        <v-row align="center" justify="center">
          <v-col cols="12" sm="8" md="4">
            <v-card class="elevation-12">
              <v-toolbar color="primary" dark flat>
                <v-toolbar-title>Registration Form</v-toolbar-title>
              </v-toolbar>
              <v-card-text>
                <v-form @submit.prevent="register">
                  <v-text-field label="Email" name="email" prepend-icon="mdi-email" type="text"/>
                  <v-text-field label="First Name" name="first_name" prepend-icon="mdi-account" type="text"/>
                  <v-text-field label="Last Name" name="last_name" prepend-icon="mdi-account" type="text"/>
                  <v-text-field
                    id="password"
                    label="Password"
                    name="password"
                    prepend-icon="mdi-lock"
                    type="password"
                  />
                  <v-text-field
                    id="password_confirmation"
                    label="Confirm Password"
                    name="password_confirmation"
                    prepend-icon="mdi-lock"
                    type="password"
                  />
                </v-form>
              </v-card-text>
              <v-card-actions>
                <v-spacer/>
                <v-btn type="submit" color="primary">Register</v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-content>
  </div>
</template>

<script>
    export default {
        middleware: 'guest',
        head() {
            return {
                title: "Register - Baseplate API"
            }
        },
        data() {
            return {
                email: '',
                first_name: '',
                last_name: '',
                password: '',
                password_confirmation: '',
            }
        },
        methods: {
            async register() {
                try {
                    await this.$axios.post('register', {
                        email: this.email,
                        firs_name: this.firs_name,
                        last_name: this.last_name,
                        password: this.password,
                        password_confirmation: this.password_confirmation
                    });

                    await this.$auth.loginWith('local', {
                        data: {
                            email: this.email,
                            password: this.password
                        }
                    });

                    this.$router.push('/user/profile');
                } catch (e) {
                    console.log(e);
                }
            }
        }
    };
</script>
