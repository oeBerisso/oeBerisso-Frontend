<template>
  <sui-container class='form-container'>
    <sui-dimmer :active="saving">
      <sui-loader size="medium">cargando</sui-loader>
    </sui-dimmer>
      <h1 style='text-align: center'>Regístrate</h1>
      <sui-segment raised>
        <sui-form @submit.prevent="handleSubmit">
        <sui-form-fields fields="three">
          <sui-form-field required :error="(errors.username || []).length > 0">
            <label>Usuario</label>
            <ErrorWrapper :errors="errors.username">
              <sui-input
                placeholder="Usuario"
                v-model="user.username"
                required
                icon-position="left"
                icon="user"
              />
            </ErrorWrapper>
          </sui-form-field>
          <sui-form-field required :error="(errors.password || []).length > 0">
            <label>Contraseña</label>
            <ErrorWrapper :errors="errors.password">
              <sui-input
                placeholder="Contraseña"
                type="password"
                v-model="user.password"
                minlength="6"
                required
                icon-position="left"
                icon="lock"
              />
            </ErrorWrapper>
          </sui-form-field>
          <sui-form-field required :error="(errors.confirm_password || []).length > 0">
            <label>Confirmar contraseña</label>
            <ErrorWrapper :errors="errors.confirm_password">
              <sui-input
                placeholder="Confirmar contraseña"
                type="password"
                minlength="6"
                v-model="user.confirm_password"
                required
                icon-position="left"
                icon="lock"
              />
            </ErrorWrapper>
          </sui-form-field>
        </sui-form-fields>
        <sui-form-fields fields='two'>
          <sui-form-field required :error="(errors.first_name || []).length > 0">
            <label>Nombre</label>
            <ErrorWrapper :errors="errors.first_name">
              <sui-input
                placeholder="Nombre"
                v-model="user.first_name"
                required
                icon-position="left"
                icon="user circle"
              />
            </ErrorWrapper>
          </sui-form-field>
          <sui-form-field required :error="(errors.last_name || []).length > 0">
            <label>Apellido</label>
            <ErrorWrapper :errors="errors.last_name">
              <sui-input
                placeholder="Apellido"
                v-model="user.last_name"
                required
                icon-position="left"
                icon="user circle"
              />
            </ErrorWrapper>
          </sui-form-field>
        </sui-form-fields>
        <sui-form-field required :error="(errors.email || []).length > 0">
          <label>Email</label>
          <ErrorWrapper :errors="errors.email">
            <sui-input
              placeholder="Email"
              type="email"
              v-model="user.email"
              required
              icon-position="left"
              icon="envelope outline"
            />
          </ErrorWrapper>
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
import ErrorWrapper from '../Fields/ErrorWrapper.vue';

export default {
  components: {
    ErrorWrapper,
  },
  name: 'register',
  methods: {
    handleSubmit: async function register() {
      this.saving = true;
      try {
        await axios({
          url: '/register',
          method: 'post',
          data: this.user,
        }).then((r) => (console.log(r)));
      } catch (e) {
        this.errors = e.response.data.errors;
      } finally {
        this.saving = false;
      }
    },
  },
  data() {
    return {
      errors: {
        username: [],
        first_name: [],
        last_name: [],
        email: [],
        password: [],
        confirm_password: [],
      },
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
