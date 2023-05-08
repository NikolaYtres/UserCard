<template>
  <div>
    <div>
      <inputForm @create-user="createUser"> </inputForm>
    </div>
    <div class="userCard" v-if="isVisible">
      <userCard
        v-for="(item, index) in userList"
        :key="index"
        :name="item.name"
        :description="item.description"
        :src="item.src"
        @brisi="brisi"
      >
      </userCard>
    </div>
    <div class="userCard" v-else>Nema prijavljenog korisnika</div>
  </div>
</template>

<script setup>
import inputForm from './components/InputForm.vue'
import userCard from './components/UserCard.vue'
import { ref } from 'vue'

const isVisible = ref(true)

const userList = ref([
  // {
  //   name: 'Nikola Hegedić',
  //   description: 'Programer',
  //   src: 'https://www.w3schools.com/howto/img_avatar.png'
  // }
])

// provjera
userExist()

//alert(userList.value.length)

function createUser(prim, description, src) {
  // provjera da li već postoji isti korisnik

  var ind = userList.value.findIndex((n) => n.name === prim)

  if (ind != -1) {
    alert('Korisnik već postoji')
    return
  }

  // dodavanje novog usera na listu
  const newUser = {
    name: prim,
    description: description,
    src: src
  }
  // add new user in a list of users
  userList.value.push(newUser)

  userExist()
  // alert('Dodan je novi korisnik ' + prim)
}
function brisi(prim) {
  // find user for delete
  var ind = userList.value.findIndex((n) => n.name === prim)
  // delete user
  userList.value.splice(ind, 1)
  userExist()
  //alert('Obrisan je: ' + prim + +ind)
}

function userExist() {
  // ako je lista prazna
  if (userList.value.length < 1 || userList.value == undefined) {
    isVisible.value = false
  } else {
    isVisible.value = true
  }
  // alert('da li postoiji ' + isVisible.value)
}
</script>

<style>
.userCard {
  display: flex;
  padding: 15px 10px;
}
</style>
