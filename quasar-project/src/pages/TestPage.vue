<template>
  <q-page padding>
    <!-- content -->

  <h1>{{ poruka }}</h1>
  <p v-html="tijelo"></p>
  <p v-text="htmlText"></p>
  <p v-html="htmlText"></p>
  
  <p v-for="item in days" :key="item">
    <button>
      {{ item }}
    </button>
    >
  </p>

  <p v-for="item in days" :key="item">
    <button v-if="item=='Ponedjeljak'">
      {{ item }}*
    </button>
    <button v-else>
      {{ item }}
    </button>
  </p>

  <a :href="link.url" :target="link.target"> {{link.text}} </a>

  <q-input color="green" v-model="text" label="Ime" @keyup="log()"> </q-input>
  <q-input color="red" v-model="text1" label="Ime"> </q-input>
  </q-page>
</template>

<script setup>
//

const link = {
url: 'http://www.google.com',
target: '_blank',
text: 'Google'
}

import { ref } from 'vue'
const text = ref('')
text.value = "Petra"

const text1 = ref('')
text1.value = "Lorenco!"

function log() {
  console.log(text.value)
}


  const poruka="TEST PAGE"
  const tijelo="Tekst na stranici"
  const htmlText="<p><b>Formatirani tekst</b> na stranici </p>"
  const days = ['Ponedjeljak', 'Utorak', 'Petak', 'Subota']

</script>