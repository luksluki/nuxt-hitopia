<template>
  <v-container>
    <section>
      <h1 class="mx-auto">Program Find Balanced Bracket</h1>
      <v-card class="pa-4">
        <v-text-field
          v-model="string"
          color="#3778f3"
          label="Masukan string"
          variant="outlined"
        ></v-text-field>
        <v-btn
          class="text-none mb-4"
          color="#3778f3"
          block
          size="x-large"
          variant="outlined"
          @click="process(string)"
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
const output = ref("");

function process(str) {
  output.value = isBalanced(str);
}

function isBalanced(str) {
  const stack = [];

  for (let i = 0; i < str.length; i++) {
    const char = str[i];

    if (char === "(" || char === "{" || char === "[") {
      stack.push(char);
    } else if (char === ")" || char === "}" || char === "]") {
      if (stack.length === 0) {
        return "NO";
      }

      const top = stack.pop();
      console.log("stack, char, top", stack, char, top);

      if (
        (char === ")" && top !== "(") ||
        (char === "}" && top !== "{") ||
        (char === "]" && top !== "[")
      ) {
        return "NO";
      }
    } else {
      return "Input yang diperbolehkan adalah sebagai berikut: ( , ) , { , } , atau [ , ]. ";
    }
  }
  if (stack.length === 0) {
    return "YES";
  } else {
    return "NO";
  }
}

function isBalanced2(str) {
  const pairs = {
    "(": ")",
    "{": "}",
    "[": "]",
  };

  const stack = [];

  for (let i = 0; i < str.length; i++) {
    const char = str[i];
    if (char in pairs) {
      stack.push(char);
    } else {
      const top = stack.pop();
      if (pairs[top] !== char) {
        return "NO";
      }
    }
  }

  return stack.length === 0 ? "YES" : "NO";
}
</script>
