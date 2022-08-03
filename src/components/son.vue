<!-- 这是一个字组件 -->
<template>
  <div>这是一个子组件{{ pos.num }}</div>
  <button @click="buttonclick">子组件的按钮</button>
  <!-- 复选框区域 -->
  <div><input type="checkbox" v-model="allcheck" name="" id="" /> 全选</div>
  <div v-for="(item, index) in allchecklist" :key="index">
    <input type="checkbox" v-model="item.value" name="" id="" /> {{ item.name }}
  </div>
</template>

<script setup lang="ts">
import { computed } from "@vue/reactivity";
import { defineProps, defineEmits, reactive, watch } from "vue";
const pos = defineProps({
  num: {
    type: Number,
    default: 20,
  },
});
// const allcheck = ref(false);
const allchecklist = reactive([
  {
    name: "选择框一",
    value: false,
  },
  {
    name: "选择框二",
    value: false,
  },
  {
    name: "选择框三",
    value: false,
  },
  {
    name: "选择框四",
    value: false,
  },
]);
console.log(allchecklist.every((item) => !item.value));
// const allcheck = computed(() => {
//   //   console.log(allchecklist.map((item) => item.value));
//   return allchecklist.every((item) => item.value);
// });

const allcheck = computed({
  get() {
    return allchecklist.every((item) => item.value);
  },
  set(newval: boolean) {
    // allcheck 被修改时执行set的代码
    allchecklist.forEach((item) => {
      // console.log(item);
      item.value = newval;
    });
  },
});
// watch(allcheck, (nv, ov) => {
//   allchecklist.forEach((item) => {
//     // console.log(item);
//     item.value = nv;
//   });
// });
const emit = defineEmits<{
  (event: "sonhd", id: string, name: number): void;
}>();
const buttonclick = () => {
  console.log("click_button");
  emit("sonhd", "id", pos.num);
};
console.log(pos);
</script>

<style lang="scss" scoped></style>
