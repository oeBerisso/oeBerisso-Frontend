<template>
  <sui-container class='form-container'>
    <sui-dimmer :active="saving">
      <sui-loader size="medium">cargando</sui-loader>
    </sui-dimmer>
    <h1 style='text-align: center'>Regístrate</h1>
    <sui-segment raised>
      <sui-form @submit.prevent="handleSubmit">
       <sui-form-fields fields="three">
          <sui-form-field required>
            <label>Usuario</label>
            <sui-input
              placeholder="Usuario"
              v-model="user.username"
              required
              icon-position="left"
              icon="user"
            />
          </sui-form-field>
          <sui-form-field required>
            <label>Contraseña</label>
            <sui-input
              placeholder="Contraseña"
              type="password"
              v-model="user.password"
              required
              icon-position="left"
              icon="lock"
            />
          </sui-form-field>
          <sui-form-field required>
            <label>Confirmar contraseña</label>
            <sui-input
              placeholder="Confirmar contraseña"
              type="password"
              v-model="user.confirm_password"
              required
              icon-position="left"
              icon="lock"
            />
          </sui-form-field>
        </sui-form-fields>
        <sui-form-fields fields='two'>
          <sui-form-field required>
            <label>Nombre</label>
            <sui-input
              placeholder="Nombre"
              v-model="user.first_name"
              required
              icon-position="left"
              icon="user circle"
            />
          </sui-form-field>
          <sui-form-field required>
            <label>Apellido</label>
            <sui-input
              placeholder="Apellido"
              v-model="user.last_name"
              required
              icon-position="left"
              icon="user circle"
            />
          </sui-form-field>
        </sui-form-fields>
        <sui-form-field required>
          <label>Email</label>
          <sui-input
            placeholder="Email"
            type="email"
            v-model="user.email"
            required
            icon-position="left"
            icon="envelope outline"
          />
        </sui-form-field>
        <sui-button fluid primary>
          Registrarse
        </sui-button>
      </sui-form>
    </sui-segment>
  </sui-container>
</template>

<script>
import axios from '../../helper/axios';
import User from '../../models/user';

export default {
  name: 'register',
  methods: {
    handleSubmit() {
      this.saving = true;
      try {
        axios({
          url: '/categories',
          method: 'post',
          data: this.user,
        });
      } catch (e) {
        console.log(e);
      } finally {
        this.saving = false;
      }
    },
  },
  data() {
    return {
      user: new User(),
      saving: false,
    };
  },
};
</script>

<style>
  .form-container {
    margin-top: 1rem!important;
    margin-bottom: 1rem!important;
    text-align: center;
  }
</style>
