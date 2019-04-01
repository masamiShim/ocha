<template>
  <v-form ref="form" v-model="valid" lazy-validation>
    <v-container>
      <v-layout>
        <v-flex
          xs12
          md4
        >
          <h2>プロフィール編集</h2>
          <v-alert
            xs12
            md5
            :value="warn"
            type="warning"
          >
            入力に誤りがあります。
          </v-alert>
          <v-alert
            xs12
            md5
            :value="success"
            type="success"
          >
            登録しました。
          </v-alert>
          <v-text-field
            v-model="name"
            :rules="nameRules"
            :conter="20"
            label="名前"
            required
          />
          <v-text-field
            v-model="age"
            :rules="ageRules"
            label="年齢"
            required
          />
          <v-btn
            :disabled="!valid"
            color="success"
            @click="save">
            登録する
          </v-btn>
        </v-flex>
      </v-layout>
    </v-container>
  </v-form>
</template>

<script>
  import { VForm, VContainer, VLayout, VFlex, VTextField, VBtn } from 'vuetify/lib'

  export default {
    name: 'OchaProfileEdit',
    components: {
      VForm, VContainer, VLayout, VFlex, VTextField, VBtn
    },
    data: () => ({
      valid: false,
      warn: false,
      success: false,
      name: '',
      age: 18,
      nameRules: [
        v => !!v || '入力してください',
        v => v.length <= 20 || '20文字以内で入力してください'
      ],
      ageRules: [
        v => !!v || '入力してください',
        v => v > 17 || '18歳未満はご利用できません'
      ]
    }),
    methods: {
      save() {
        if (!this.$refs.form.validate()) {
          this.warn = true
          setTimeout(() => {
            this.warn = false
          }, 1000)
          return
        }
        localStorage.setItem('ocha.profile', JSON.stringify({ name: this.name, age: this.age }))
        this.success = true
        setTimeout(() => {
          this.success = false
        }, 1000)
      }
    },
    created() {
      const exists = localStorage.getItem('ocha.profile')
      if (!exists) {
        return
      }

      const { name, age } = JSON.parse(exists)
      this.name = name
      this.age = age
    }
  }
</script>

<style scoped>

</style>
