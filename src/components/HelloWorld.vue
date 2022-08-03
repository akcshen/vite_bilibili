<script setup lang="ts">
import sonDom from "./son.vue";
import { ref, onMounted, nextTick, watch } from "vue";
let hDome = ref();
let num = ref(10);
console.log(hDome.value);
onMounted(() => {
  console.log(hDome.value);
});
nextTick(() => {
  console.log("nextTick", hDome.value);
});
watch(num, (newval, oldval) => {
  console.log(newval, oldval);
});
const numhd = () => {
  // console.log(11);
  // console.log(num.value);
  num.value++;
};
const numhd1 = (par: string, n: number) => {
  console.log(par, n, "sonhd");
  // console.log(11);
  console.log(num.value);
  num.value += 5;
};
defineProps<{ msg: string }>();

const count = ref(0);
</script>

<template>
  <sonDom :num="num" @sonhd="numhd1"></sonDom>
  <h1 ref="hDome" @click="numhd">111{{ msg }}</h1>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
