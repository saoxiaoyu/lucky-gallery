<script setup lang="ts">
const emit = defineEmits(['closeLogin'])
const { fetch: refreshSession } = useUserSession()
const password = ref('')
const loading = ref(false)

const toast = useToast()

async function login() {
  if (loading.value || !password.value) return
  loading.value = true
  await $fetch('/api/auth', {
    method: 'POST',
    body: { password: password.value }
  })
    .then(async () => {
      await refreshSession()
      emit('closeLogin')
    })
    .catch((err) => {
      toast.add({
        title: `Error ${err.statusCode}`,
        description: `${err.data?.message || err.message}. Please try again`,
        color: 'red'
      })
    })
  loading.value = false
}
</script>

<template>
  <form
    class="flex flex-col gap-y-4 p-4 items-center"
    @submit.prevent="login"
  >
    <h1 class="text-lg text-gray-300">
      登录以上传图片
    </h1>
    <UInput
      v-model="password"
      type="password"
      placeholder="管理员密码"
      icon="i-heroicons-key"
      class="!w-60"
    />

    <UButton
      :loading="loading"
      type="submit"
      label="登录"
      color="blue"
      variant="ghost"
      class="px-4"
      size="lg"
      :disabled="!password"
    />
  </form>
</template>
