<script setup>
// <script setup> is a compile-time syntactic sugar for using Composition API inside Single-File Components (SFCs).
// It is the recommended syntax if you are using both SFCs and Composition API. It provides a number of advantages over the normal <script> syntax.
// defineProps and defineEmits are compiler macros only usable inside <script setup>.
// They do not need to be imported, and are compiled away when <script setup> is processed.

import { ref } from 'vue'

defineProps({
  message: String,
})

// I can also store them in a variable
// const props =  defineProps({
//   message: String,
//   required: true
// })

defineEmits(['update-message-clicked'])

const count = ref(0)
</script>

<template>
  <h1>Message: {{ message }}</h1>
  <button @click="$emit('update-message-clicked')">Change message</button>

  <div class="card">
    <button type="button" @click="count++">count is {{ count }}</button>
    <p>
      Edit
      <code>components/HelloWorld.vue</code> to test HMR
    </p>
  </div>

  <p class="text-green-600">
    Check out
    <a href="https://vuejs.org/guide/quick-start.html#local" target="_blank"
      >create-vue</a
    >, the official Vue + Vite starter
  </p>
  <p class="text-green-800 text-right bg-green-200">
    Install
    <a href="https://github.com/vuejs/language-tools" target="_blank">Volar</a>
    in your IDE for a better DX
  </p>
  <p class="read-the-docs">Click on the Vite and Vue logos to learn more</p>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
