<template>
    <div id="app">
  <v-app id="inspire">
    <v-app id="inspire">
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
              <v-card class="elevation-12">
                <v-toolbar
                  color="primary"
                  dark
                  flat
                >
                  <v-toolbar-title>Recruiter Login</v-toolbar-title>
                  <v-spacer></v-spacer>
                  <v-icon large>mdi-account</v-icon>
                </v-toolbar>
                <v-card-text>
                  <v-form ref="form" v-model="valid">
                    <v-text-field
                      label="Login"
                      name="login"
                      prepend-icon="mdi-account"
                      type="text"
                      v-model="username"
                      :rules="[v => (v || '').length >= 2 || 'Atleast 2 characters required']"
                    ></v-text-field>
                    <v-text-field
                      id="password"
                      label="Password"
                      name="password"
                      prepend-icon="mdi-lock"
                      type="password"
                      v-model="password"
                    ></v-text-field>
                  </v-form>
                </v-card-text>
                <v-card-actions>
                  <v-spacer></v-spacer>
                  <span class="red--text ml-12">{{msg}}</span>
                  <v-spacer></v-spacer>
                  <v-btn color="primary" @click="login" :loading="loading">Login</v-btn>
                </v-card-actions>
              </v-card>
            </v-col>
          </v-row>
        </v-container>
      </v-main>
    </v-app>
  </v-app>
</div>
</template>
<script>
import { mapState, mapActions } from 'vuex'
export default {
  name: 'login',
  data: () => ({
    valid: true,
    username: '',
    password: '',
    msg: '',
    loading: false
  }),
  computed: { ...mapState(['recruiter']) },
  methods: {
    ...mapActions(['setRecruiter']),
    login () {
      if (this.$refs.form.validate()) {
        if (this.username === 'recruiter' && this.password === 'password') {
          this.loading = true
          this.setRecruiter(this.username)
          setTimeout(() => {
            this.loading = false
            this.$router.push('dashboard')
          }, 1000)
        } else {
          this.msg = 'Incorrect username or password'
        }
      }
    }
  },
  mounted () {
    if (this.recruiter) {
      this.$router.push('dashboard')
    }
  }
}
</script>
