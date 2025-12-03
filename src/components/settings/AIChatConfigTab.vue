<script setup lang="ts">
import { ref, watch } from 'vue'
import { useChatStore } from '@/stores/chat'
import { storeToRefs } from 'pinia'

const emit = defineEmits<{
  'config-changed': []
}>()

const chatStore = useChatStore()
const { aiGlobalSettings } = storeToRefs(chatStore)

// 本地状态
const maxMessages = ref(aiGlobalSettings.value.maxMessagesPerRequest)
const isSaving = ref(false)

// 保存配置
async function saveConfig() {
  isSaving.value = true
  try {
    chatStore.updateAIGlobalSettings({
      maxMessagesPerRequest: maxMessages.value,
    })
    emit('config-changed')
  } finally {
    isSaving.value = false
  }
}

// 监听 store 变化
watch(
  () => aiGlobalSettings.value.maxMessagesPerRequest,
  (newVal) => {
    maxMessages.value = newVal
  }
)
</script>

<template>
  <div class="space-y-6">
    <!-- 标题 -->
    <h3 class="mb-3 flex items-center gap-2 text-sm font-semibold text-gray-900 dark:text-white">
      <UIcon name="i-heroicons-chat-bubble-left-right" class="h-4 w-4 text-primary-500" />
      AI 聊天配置
    </h3>

    <div class="space-y-4 rounded-lg border border-gray-200 bg-gray-50 p-4 dark:border-gray-700 dark:bg-gray-800/50">
      <!-- 上下文消息数量 -->
      <div>
        <label class="mb-2 block text-sm font-medium text-gray-700 dark:text-gray-300">上下文消息数量</label>
        <div class="flex items-center gap-4">
          <URange v-model="maxMessages" :min="10" :max="1000" :step="10" class="flex-1" />
          <UInput v-model.number="maxMessages" type="number" class="w-24" />
        </div>
        <p class="mt-1 text-xs text-gray-500">
          每次发送给 AI 的历史消息数量（10-1000）。数量越多，AI 了解的上下文越多，但消耗的 Token 也越多。
        </p>
      </div>

      <!-- 保存按钮 -->
      <div class="flex justify-end pt-2">
        <UButton color="primary" :loading="isSaving" @click="saveConfig">保存配置</UButton>
      </div>
    </div>
  </div>
</template>
