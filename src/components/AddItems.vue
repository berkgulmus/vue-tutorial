<script setup lang="ts">
  import { inject, ref } from 'vue'
  const newItemText = ref('')
  const emit = defineEmits(['addItem'])
  const addItemInAncestor = inject('addItemInAncestor') as (a: string) => void
  const formatText = (prefix?: string) => {
    return (prefix ?? '') + newItemText.value
  }
  const addItemByEmitting = (prefix?: string) => {
    emit('addItem', formatText(prefix))
  }
  const addItemDirectly = (prefix?: string) => {
    addItemInAncestor(formatText(prefix))
  }
</script>

<template>
  <div class="add-form">
    <h1>Add list item here!</h1>
    <input
      type="text"
      v-model="newItemText"
      @keyup.enter="() => addItemByEmitting('Added by pressing Enter -> ')"
    />
    <button @click="() => addItemByEmitting(`Added from Button -> `)">
      Add Item by emitting event!
    </button>
    <button @click="() => addItemDirectly(`Added directly using provide-inject -> `)">
      Add Item directly!
    </button>
  </div>
</template>

<style>
  .add-form {
    display: flex;
    flex-direction: column;
    gap: 15px;
    justify-self: center;
  }
</style>
