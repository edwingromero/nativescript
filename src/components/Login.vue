<template>
  <Page actionBarHidden="true">
    <StackLayout verticalAlignment="center">
      <Image src="~/assets/images/logo.png" width="150" class="m-b-30"></Image>
      <Label class="h1 text-center"  text="Bienvenido" />
      <StackLayout class="nt-input">
        <Label text="Email" class="font-weight-bold m-b-5" />
        <TextField v-model="email" />
        <Label v-if="$v.email.$error && !$v.email.required" text="Es requerido" class="text-danger" />
        <Label v-if="$v.email.$error && !$v.email.email" text="No un email valido" class="text-danger" />
      </StackLayout>
      <StackLayout class="nt-input">
        <Label text="Contraseña" class="font-weight-bold m-b-5" />
        <TextField v-model="contrasena" secure="true" />
        <Label v-if="$v.contrasena.$error && !$v.contrasena.required" text="Es requerido" class="text-danger" />
        <Label v-if="$v.contrasena.$error && !$v.contrasena.minLength" text="Mínimo 8 caracteres" class="text-danger" />
      </StackLayout>
      
      <Button v-if="!disabledButton" class="-primary" text="Iniciar Sesión" @tap="iniciarSesion" />

      <Button v-if="disabledButton" class="-primary" text="Procesando" />
    </StackLayout> 
</Page>
</template>

<script >


import { required, minLength, email } from 'vuelidate/lib/validators'
import axios from "axios/dist/axios";
import {getString, setString, remove} from 'tns-core-modules/application-settings'

export default {
  data() {
    return {
      email: 'edwing8957@gmail.com',
      contrasena:'12345678',
      token: '',
      disabledButton:false
    };
  },
  validations: {
    email: {
      required,
      email
    },
    contrasena: {
      required,
      minLength: minLength(6)
    }
  },
  mounted() {
    if(getString("token")!=''){
      //this.$navigateTo(Home)
    }
  },
  methods: {
    cerrarSesion () {
      remove("token");
    },
    iniciarSesion(){
      let vue = this;
      vue.disabledButton = true;
      vue.$v.$touch();
      if (!this.$v.$invalid) {
        vue.$navigator.navigate('/home',{ clearHistory: true })
        /*axios.post('http://c47418e3a3b3.ngrok.io/api/auth/login',{
          email:vue.email,
          password:vue.contrasena,
          remember_me:true
        })
        .then(res => {
          vue.disabledButton = false;
          vue.token = res.data.access_token;
          setString('token', vue.token);
          this.$navigateTo(Home)
        })
        .catch(err => {
          vue.disabledButton = false;
          alert('error');
        })*/
      }
    }
  }
}
</script>

<style>
    ActionBar {
        background-color: #53ba82;
        color: #ffffff;
    }

    TextField{
      font-size:16
    }

    Button{
      font-size:16
    }

    .title {
        text-align: left;
        padding-left: 16;
    }

    .message {
        vertical-align: center;
        text-align: center;
        font-size: 20;
        color: #333333;
    }

    .drawer-header {
        padding: 16 16 16 16;
        margin-bottom: 5;
        background-color: #53ba82;
        color: #ffffff;
        font-size: 24;
    }

    .drawer-item {
        padding: 8 16;
        color: #333333;
        font-size: 16;
    }
</style>
