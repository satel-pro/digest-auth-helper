<template>
  <div style="display: flex; text-align: left;">
    <div class="col">
      <div>username: <input v-model="username" type="text" /></div>
      <div>realm: <input v-model="realm" type="text" /></div>
      <div>password: <input v-model="password" type="text" /></div>
      <div>nonce: <input v-model="nonce" type="text" /></div>
      <div>method: <input v-model="method" type="text" /></div>
      <div>uri: <input v-model="uri" type="text" /></div>
    </div>
    <div class="col">
      <div>HA1: <input readonly :value="ha1" type="text" /> </div>
      <div>HA2: <input readonly :value="ha2" type="text" /></div>
      <div>RESULT: <input readonly :value="result" type="text" /></div>
    </div>
  </div>
  <div>
    <textarea></textarea>
  </div>
</template>
<script setup lang="ts">
import md5 from 'md5'
import { computed, ref } from 'vue'

const username = ref('Xt73Oxs1')
const realm = ref('REGISTRAR')
const password = ref('Uk6z3NGt')
const nonce = ref('4AC3219D')
const method = ref('SUBSCRIBE')
const uri = ref('')

const ha1 = computed(() => {
  return md5(`${username.value}:${realm.value}:${password.value}`)
})

const ha2 = computed(() => {
  return md5(`${method.value}:${uri.value}`)
})

const result = computed(() => {
  return md5(`${ha1.value}:${nonce.value}:${ha2.value}`)
})
</script>
<style scoped>
.col {
  padding: 10px;
  width: 500px;
}
.col input {
  margin-left: 10px;
  width: 400px;
  display: block;
  margin-bottom: 10px;
}
</style>
