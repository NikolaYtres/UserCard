<template>
  <div class="user-form">
    <input
      class="user-form__input"
      type="text"
      placeholder="Molimo unesite ime i prezime"
      name="prim"
      id="prim"
      v-model="prim"
    />
    <input
      class="user-form__input"
      type="text"
      placeholder="Molimo unesite opise"
      name="description"
      id="description"
      v-model="description"
    />
    <input
      class="user-form__input"
      type="text"
      placeholder="Molimo unesite URL za sliku"
      name="src"
      id="src"
      v-model="src"
    />
    <button class="user-form__buttonAdd" @click="createUser">Dodaj korisnika</button>
  </div>

  <div></div>
</template>

<script setup>
import { ref } from 'vue'

const prim = ref()
const description = ref()
const src = ref()
const emit = defineEmits(['createUser'])

function createUser() {
  if (prim.value == '' || prim.value == undefined) {
    alert('Niste upisali ime')
    return
  }
  if (description.value == '' || description.value == undefined) {
    alert('Niste upisali opis')
    return
  }
  if (src.value == '' || src.value == undefined) {
    alert('Niste upisali URL')
    return
  }

  // provjera URL-a

  const isValidUrl = (src) => {
    var urlPattern = new RegExp(
      '^(https?:\\/\\/)?' + // validate protocol
        '((([a-z\\d]([a-z\\d-]*[a-z\\d])*)\\.)+[a-z]{2,}|' + // validate domain name
        '((\\d{1,3}\\.){3}\\d{1,3}))' + // validate OR ip (v4) address
        '(\\:\\d+)?(\\/[-a-z\\d%_.~+]*)*' + // validate port and path
        '(\\?[;&a-z\\d%_.~+=-]*)?' + // validate query string
        '(\\#[-a-z\\d_]*)?$',
      'i'
    ) // validate fragment locator
    return !!urlPattern.test(src.value)
  }

  //alert('da li je validan? ' + isValidUrl(src))

  if (!isValidUrl(src)) {
    alert('URL nije ispravan!')
    return
  }

  // emit eventa
  emit('createUser', prim.value, description.value, src.value)
  // clean inputs
  resetinput()
}
function resetinput() {
  prim.value = ''
  description.value = ''
  src.value = ''
}
</script>

<style>
.user-form {
  display: flex;
}
.user-form__input {
  padding: 15px 10px;
  width: 300px;
}
.user-form__buttonAdd {
  padding: 10px 15px;
  width: 100px;
}
</style>
