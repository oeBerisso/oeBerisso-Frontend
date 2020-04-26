<template>
  <sui-container class='form-container'>
     <sui-grid centered vertical-align="middle">
      <sui-grid-column>
        <h2 is="sui-header">
          <sui-header-content>Inicia sesión</sui-header-content>
        </h2>
        <sui-form @submit.prevent="handleSubmit">
          <sui-segment stacked>
            <sui-form-field>
              <label>Usuario</label>
              <sui-input
                placeholder="Usuario"
                icon="user"
                v-model="user.username"
                required
                icon-position="left"
              />
            </sui-form-field>
            <sui-form-field>
              <label>Contraseña</label>
              <sui-input
                type="password"
                placeholder="Contraseña"
                icon="lock"
                required
                icon-position="left"
              />
            </sui-form-field>
            <sui-button size="large" primary fluid>Inicia sesión</sui-button>
          </sui-segment>
        </sui-form>

        <sui-message>
          ¿No poseés cuenta?
          <a href="/registrarse">Registrate aqui</a>
        </sui-message>
      </sui-grid-column>
    </sui-grid>
  </sui-container>
</template>

<script>
import User from '../../models/user';

export default {
  name: 'login',
  methods: {
    handleSubmit() {
      console.log(this.user);
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

<style lang='scss'>
  .form-container {
    margin-top: 1rem!important;
    margin-bottom: 1rem!important;

    .grid {
      height: 100%;
    }
    .column {
      max-width: 450px;
      text-align: center !important;
    }
  }

</style>
