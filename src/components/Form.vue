<template>
  <div class="jumbotron">
    <vue-form :state="formState" @submit.prevent="send()">
      <validate tag="div">
        <label for="name">Nombre</label>
        <input
          class="form-control"
          type="text"
          id="name"
          name="name"
          v-model.trim="formData.name"
          autocomplete="off"
          :minlength="minNameLength"
          :maxlength="maxNameLength"
          required
        />
        <field-messages name="name" show="$dirty">
          <div slot="required" class="alert alert-danger mt-1">
            Campo requerido
          </div>
          <div slot="minlength" class="alert alert-danger mt-1">
            Este campo requiere {{ minNameLength }} caracteres como mínimo
          </div>
          <div
            v-if="formData.name.length === maxNameLength"
            class="alert alert-warning mt-1"
          >
            Máximo {{ maxNameLength }} caracteres
          </div>
        </field-messages>
      </validate>
      <validate tag="div">
        <label for="age">Edad</label>
        <input
          class="form-control"
          type="number"
          id="age"
          :min="minAge"
          :max="maxAge"
          name="age"
          v-model.number="formData.age"
          autocomplete="off"
          required
        />
        <field-messages name="age" show="$dirty">
          <div slot="required" class="alert alert-danger mt-1">
            Campo requerido
          </div>
          <div slot="min" class="alert alert-danger mt-1">
            Edad mínima: {{ minAge }} años
          </div>
          <div slot="max" class="alert alert-danger mt-1">
            Edad máxima: {{ maxAge }} años
          </div>
        </field-messages>
      </validate>
      <validate tag="div">
        <label for="email">E-mail</label>
        <input
          class="form-control"
          type="email"
          id="email"
          name="email"
          v-model.trim="formData.email"
          autocomplete="off"
          required
        />
        <field-messages name="email" show="$dirty">
          <div slot="required" class="alert alert-danger mt-1">
            Campo requerido
          </div>
          <div slot="email" class="alert alert-danger mt-1">
            Email no válido
          </div>
        </field-messages>
      </validate>
      <button
        class="btn btn-success my-3"
        :disabled="formState.$invalid"
        type="submit"
      >
        Submit
      </button>
    </vue-form>
    <div class="table-responsive">
      <table class="table table-light">
        <tr>
          <th v-for="(col, i) in getColumnas" :key="i">{{ col }}</th>
        </tr>
        <td v-for="(v, i) in formData" :key="i">
          {{ v }}
        </td>
      </table>
    </div>
  </div>
</template>

<script lang="js">
export default {
  name: 'src-components-form',
  props: [],
  mounted() {
  },
  data() {
    return {
      formData: this.getFormInicial(),
      formState: {},
      minNameLength: 5,
      maxNameLength: 15,
      minAge: 18,
      maxAge: 100
    }
  },
  methods: {
    getFormInicial() {
      return {
        name: '',
        age: '',
        email: ''
      }
    },
    send() {
      this.formData = this.getFormInicial()
       this.formState._reset()
    },
  },
  computed: {
    getColumnas() {
      return Object.keys(this.formData)
    }
  }
}
</script>
