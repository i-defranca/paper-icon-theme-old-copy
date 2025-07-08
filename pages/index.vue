<template>
  <div class="flex flex-col gap-2">
    <button type="button" class="btn-outline" @click="copy">Copy</button>
    <button type="button" class="btn-outline" @click="copy(false)">Don't wait</button>
  </div>
</template>
<script setup lang="ts">
const toast = useToast()
const loading = ref<boolean>(false)

const copy = async (wait = true) => {
  try {
    loading.value = true

    await new Promise(resolve => setTimeout(resolve, 2000))
    if (wait) {
      await navigator.clipboard.writeText('clipboard test')
    } else {
      navigator.clipboard.writeText('clipboard test')
    }

    toast.success({ message: 'Clipboard success' })
  } catch (error) {
    let message = 'Clipboard error'

    if (error?.name == 'NotAllowedError') {
      message = 'Clipboard not allowed'
    }

    toast.error({ message })
  } finally {
    loading.value = false
  }
}

useHead({
  title: 'index'
});
</script>

<style>
@reference '@/assets/css/main.css';

.btn-outline {
  @apply py-2 px-3 font-medium text-gray-900 bg-white rounded-lg border-2 border-orange-600 cursor-pointer;
  @apply hover:bg-gray-100 hover:text-orange-600 hover:font-bold;
  @apply focus:outline-none focus:z-10;
}
</style>
