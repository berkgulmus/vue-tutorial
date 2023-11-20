<script setup lang="ts">
  import { ref, computed, type PropType } from 'vue'
  const props = defineProps({
    listItems: {
      type: Object as PropType<string[]>,
      required: false,
      default: () => ['asdasdas'] as Object
    }
  })
  const searchText = ref('')
  const filteredItems = computed(() => {
    return props?.listItems?.filter((item: string) => item.includes(searchText.value))
  })
</script>

<template>
  <div>
    <h2>Filter items by the search input</h2>
    <input v-model="searchText" />
    <div v-if="filteredItems?.length !== 0 && searchText !== ''">
      <ul v-for="(item, index) in filteredItems" :key="index">
        {{
          item
        }}
      </ul>
    </div>
  </div>
</template>
<style lang=""></style>
