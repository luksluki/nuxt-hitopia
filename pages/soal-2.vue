<template>
  <v-container>
    <section>
      <h1 class="mx-auto">Program Find Highest Palindrome</h1>
      <v-card class="pa-4">
        <v-text-field
          v-model="string"
          color="#3778f3"
          label="Masukan string"
          variant="outlined"
        ></v-text-field>
        <v-text-field
          v-model="k"
          type="number"
          color="#3778f3"
          label="Masukan nilai k"
          variant="outlined"
        ></v-text-field>
        <v-btn
          class="text-none mb-4"
          color="#3778f3"
          block
          size="x-large"
          variant="outlined"
          @click="process(string, k)"
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
const k = ref(0);
const output = ref([]);

function process(string, k) {
  output.value = createPalindrome(string, k);
}

function createPalindrome(inputString, k) {
  const strArr = inputString.split("");
  const results = []; // Array untuk menyimpan semua kemungkinan palindrome

  function checkAndReplaceCharacters(left, right, k, palindrome) {
    if (left >= right) {
      results.push(palindrome.join(""));
      return;
    }

    if (strArr[left] !== strArr[right]) {
      if (k === 0) {
        return -1;
      }

      const updatedPalindrome = [...palindrome]; // Membuat salinan baru dari palindrome

      // Membandingkan karakter pada posisi left dan right, dan mengganti dengan yang lebih besar
      if (strArr[left] > strArr[right]) {
        updatedPalindrome[right] = updatedPalindrome[left];
      } else {
        updatedPalindrome[left] = updatedPalindrome[right];
      }

      checkAndReplaceCharacters(left + 1, right - 1, k - 1, updatedPalindrome);
    } else {
      checkAndReplaceCharacters(left + 1, right - 1, k, palindrome);
    }
  }

  checkAndReplaceCharacters(0, strArr.length - 1, k, strArr);

  return results;
}
</script>
