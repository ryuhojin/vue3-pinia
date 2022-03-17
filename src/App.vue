<template>
  <div>
    <input type="text" v-model="text" />
    <button @click="addList(text)">추가</button>
    <h4>추가된 목록</h4>
    <p v-for="(item, index) in getDataAll" :key="index">
      {{ item }}
    </p>
  </div>
</template>
<script>
import { computed, ref } from "vue";
import { useListStore } from "./stores/list";
export default {
  setup() {
    const text = ref("");
    const list = useListStore();

    function addList() {
      if (!text.value) return;
      list.$patch({ list: [...list.getDataAll, text.value] });
      text.value = "";
    }

    return {
      text,
      addList,
      getDataAll: computed(() => list.getDataAll),
    };
  },
};
</script>
