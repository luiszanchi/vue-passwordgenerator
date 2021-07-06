<template>
  <div class="home">
    <b-container class="container">
      <b-card-group deck class="mb-4">
        <b-card
          title="Tamanho"
        >
          <b-form-spinbutton 
            v-model="form.size" 
            min="1" 
            max="100"
          />
        </b-card>
        <b-card
          title="Maiúsculas"
        >
          <b-form-checkbox
            v-model="form.uppercase"
          />
        </b-card>
        <b-card
          title="Minúsculas"
        >
          <b-form-checkbox
            v-model="form.lowercase"
          />
        </b-card>
        <b-card
          title="Números"
        >
          <b-form-checkbox
            v-model="form.numeric"
          />
        </b-card>
        <b-card
          title="Caracteres Especiais"
        >
          <b-form-checkbox
            v-model="form.specialCharacters"
          />
        </b-card>
      </b-card-group>

      <b-card-group deck class="mb-4">
        <b-card
          title="Senha"
          class="password-card"
        >
          <b-form-input 
            class="password-field"
            v-model="form.password" 
            placeholder="Gere a sua senha"
            :disabled="true"
          />
          <b-button 
            variant="success"
            class="password-generate-button"
            @click="generatePassword()"
          >
            Gerar
          </b-button>
        </b-card>
      </b-card-group>
    </b-container>
  </div>
</template>

<style lang="sass" scoped>
.linha
  border: 1px solid black;
  margin-round: 5px;
  position: relative;

.linha:not(:first-child)
  border-top: unset;

.password-card
  display: inline;

.password-generate-button
  width: 100px;

.password-field
  width: calc(100% - 100px);
  display: inline-block;

label
  vertical-align: middle;
  margin-bottom: unset;
  position: absolute;
  top: 50%;
  -ms-transform: translateY(-50%);
  transform: translateY(-50%);
</style>

<script lang="ts">
// @ts-nocheck
export default {
  name: 'Home',
  data: () => ({
    form: {
      password: '',
      size: 6,
      uppercase: true,
      lowercase: true,
      numeric: true,
      specialCharacters: true,
    }
  }),
  methods: {
    range (start: number, stop: number, step = 1): Array<number> {
      return Array(Math.ceil((stop - start) / step))
        .fill(start)
        .map((x, y) => x + y * step)
    },
    generatePassword() {
      /**
       * @type {object}
       */
      this.form;

      this.form.password = '';

      while (this.form.password.length < this.form.size) {
        this.form.password += this.unionCharacters[this.getRandomNumber(this.unionCharacters.length)]
      }
    },
    getRandomNumber(max: number): number
    {
      return Math.floor(Math.random() * max);
    }
  },
  computed: {
    uppercase(): Array<string> {
      console.log('this', this);
      return this.range(65, 91).map((i: number) => String.fromCharCode(i));
    },
    lowercase(): Array<string> {
      return this.range(97, 123).map((i: number) => String.fromCharCode(i));
    },
    numeric(): Array<string> {
      return this.range(48, 58).map((i: number) => String.fromCharCode(i));
    },
    specialCharacters(): Array<string> {
      let range = [...this.range(33, 48), ...this.range(58, 65)];
      return range.map((i: number) => String.fromCharCode(i));
    },
    unionCharacters(): Array<string> {
      let chars: Array<string> = [];

      if (this.form.uppercase) {
        chars = chars.concat(this.uppercase);
      }

      if (this.form.lowercase) {
        chars = chars.concat(this.lowercase);
      }

      if (this.form.numeric) {
        chars = chars.concat(this.numeric);
      }
      /**
       * @var {Object} this - The shape is the same as SpecialType above
       * @var {Array<String>} this.specialCharacters
       */
      if (this.form.specialCharacters) {
        chars = chars.concat(this.specialCharacters);
      }

      return chars;
    }
  },
}
</script>
