<template>
  <div class="user-card">
    <img class="user-card__title-img" :src="props.src" />

    <div class="user-card__name">
      <slot name="name">{{ props.name }} </slot>
    </div>

    <div class="user-card__description">{{ props.description }}</div>

    <div class="user-card__actions">
      <button @click="brisi">Delete</button>
    </div>
  </div>
</template>

<script setup>
const props = defineProps(['name', 'description', 'src'])
const emit = defineEmits(['open', 'brisi'])

// function open() {
//   emit('open')
// }
function brisi() {
  emit('brisi', props.name)
}
</script>

<style>
.user-card {
  border: 5px solid lightgray;
  width: 250px;
  border-radius: 10px;
}
.user-card__title-img {
  width: 100%;
}
.user-card__name {
  border-top: 1px solid lightgray;
  padding: 5px 10px;
}
.user-card__description {
  border-top: 1px solid lightgray;
  padding: 5px 10px;
}
.user-card__actions {
  border-top: 1px solid lightgray;
  padding: 5px 10px;
  display: flex;
  justify-content: center;
}
</style>
