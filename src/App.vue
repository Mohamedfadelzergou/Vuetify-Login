<template>
  <v-app>
    <div class="background">

    </div>
    <v-main class="d-flex justify-center align-center">
      <v-col cols="10" lg="4" class="mx-auto">
        <v-card class="pa-4">
          <div class="text-center">
            <v-avatar
              color="indigo lighten-4"
              size="100"
            >
            <v-icon color="indigo" size="40">mdi-account</v-icon>
            </v-avatar>
            <h2 class="indigo--text">Vuetify Login Page</h2>
            <v-form @submit.prevent="submitHandeler" ref="form">
              <v-card-text>
                <v-text-field v-model="email" :rules="emailRules" type="email" label="Email" placeholder="Email" prepend-inner-icon="mdi-account"/>
                <v-text-field v-model="password" :rules="passwordRules" :type="passwordshow?'text':'password'" label="Password" placeholder="Password" prepend-inner-icon="mdi-lock" :append-icon="passwordshow ? 'mdi-eye':'mdi-eye-off'" @click:append="passwordshow = !passwordshow"/>
                <v-switch label="Remember me" color="indigo"/>
              </v-card-text>
              <v-card-actions class="justify-center">
                <v-btn :loading="louding" type="submit" color="indigo"><span class="white--text px-8">Login</span></v-btn>
              </v-card-actions>
            </v-form>
          </div>
        </v-card>
      </v-col>
    </v-main>
    <v-snackbar top color="success" v-model="snackbar">Login Success</v-snackbar>
  </v-app>
</template>

<script>

export default {
  name: 'App',

  components: {
  },

  data: () => ({
    louding:false,
    snackbar:false,
    passwordshow:false,
    password: '',
    passwordRules: [
        v => !!v || 'Password is required',
        v => (v && v.length >= 6) || 'Password must be less than 6 characters or more!',
    ],
    email: '',
    emailRules: [
        v => !!v || 'E-mail is required',
        v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
    ],
  }),
  methods:{
    submitHandeler(){
      if(this.$refs.form.validate()){
        this.louding=true
        setTimeout(() => {
          this.louding=false
          this.snackbar=true
        }, 300);
      }
    }
  }
};
</script>
<style>
.background{
  background-image: url('./assets/Order-Banner.jpg');
  display: block;
  position: absolute;
  background-size: cover;
  height: 300px;
  width: 100%;
  top:0;
}
</style>
