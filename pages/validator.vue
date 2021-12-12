<template>
  <form @submit.prevent="validate()">
    <input type="text" v-model="name">
    <input type="text" v-model="description">

    <button type="submit">validar</button>
  </form>
</template>

<script lang="ts">
import Vue from 'vue'
import Validator, { IMessages, IRules, IValues } from "@elpandev/laravel-validator";
export default Vue.extend({
  data() {
    return {
      name: '',
      description: ''
    }
  },
  methods: {
    validate() {
      const payload: IValues = {
        name:        this.name,
        description: this.description,
      }

      const rules: IRules = {
        name:        ['required'],
        description: ['required']
      }

      const messages: IMessages = {
        name:        { required: 'El campo "nombre" es requerido' },
        description: { required: 'El campo "descripción" es requerido' },
      }

      const validator = new Validator(payload, rules, messages)

      console.log(validator.errors)
    }
  }
})
</script>
