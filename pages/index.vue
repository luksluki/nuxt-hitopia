<template>
  <v-container>
    <section>
      <h1 class="mb-4">1. Program Weighted Strings</h1>
      <v-card class="pa-4">
        <v-text-field
          v-model="string"
          color="#3778f3"
          label="Masukan string"
          variant="outlined"
        ></v-text-field>
        <div class="d-flex">
          <v-text-field
            v-model.number="number"
            class="mr-2"
            rounded
            type="number"
            color="#3778f3"
            label="Masukan angka"
            variant="outlined"
          ></v-text-field>
          <v-btn
            class="text-none mr-2"
            color="#3778f3"
            size="x-large"
            variant="outlined"
            @click="addToQueries"
          >
            + to Queries
          </v-btn>
          <v-btn
            class="text-none"
            color="red"
            size="x-large"
            variant="outlined"
            @click="resetQueries"
          >
            Reset
          </v-btn>
        </div>
        <p class="font-weight-bold mb-4">Queries : {{ queries }} <br /></p>
        <v-btn
          class="text-none mb-4"
          color="#3778f3"
          block
          size="x-large"
          variant="outlined"
          @click="weightedStrings(string, queries)"
          >Proses</v-btn
        >
        <p class="font-weight-bold">Output : {{ output }}</p>
      </v-card>
    </section>
  </v-container>
</template>

<script lang="ts" setup>
import { ref } from "vue";
const string = ref("");
const queries = ref([]);
const number = ref(0);
const output = ref([]);

function addToQueries() {
  queries.value.push(number.value);

  // Reset nilai input setelah ditambahkan ke queries
  number.value = 0;
}

function resetQueries() {
  queries.value = [];
  number.value = 0;
}

function weightedStrings(string, queries) {
  const weights = {}; // objek untuk menyimpan bobot setiap substring atau karakter
  const result = []; // array untuk menyimpan status dari setiap query

  // Membuat bobot untuk setiap karakter dan substring dalam string
  for (let i = 0; i < string.length; i++) {
    const weight = string.charCodeAt(i) - "a".charCodeAt(0) + 1;
    weights[string[i]] = weight;
    console.log(weight, weights);

    // Mengecek jika ada karakter yang berulang dan berurutan
    let j = i + 1;
    while (j < string.length && string[j] === string[i]) {
      const substring = string.slice(i, j + 1);
      const substringWeight =
        (j - i + 1) * (string.charCodeAt(i) - "a".charCodeAt(0) + 1);
      weights[substring] = substringWeight;
      j++;
    }
  }

  // Memeriksa status dari setiap query
  for (let i = 0; i < queries.length; i++) {
    const query = queries[i];
    if (Object.values(weights).includes(query)) {
      result.push("Yes");
    } else {
      result.push("No");
    }
  }

  output.value = result;
}
</script>
