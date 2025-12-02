<script setup lang="ts">
import { ref } from 'vue'
import { SubTabs } from '@/components/UI'
import MergeTab from '@/components/tools/MergeTab.vue'

// Tab 配置
const tabs = [{ id: 'merge', label: '合并聊天记录', icon: 'i-heroicons-document-duplicate' }]

const activeTab = ref('merge')
</script>

<template>
  <div class="flex h-full flex-col bg-gray-50 dark:bg-gray-950">
    <!-- Header -->
    <div class="border-b border-gray-200 bg-white px-6 py-4 dark:border-gray-800 dark:bg-gray-900">
      <h1 class="text-xl font-semibold text-gray-900 dark:text-white">实用工具</h1>
      <p class="mt-1 text-sm text-gray-500 dark:text-gray-400">提供聊天记录处理的实用工具</p>
    </div>

    <!-- Tabs -->
    <SubTabs v-model="activeTab" :items="tabs" />

    <!-- Tab Content -->
    <div class="flex-1 overflow-auto p-6">
      <MergeTab v-if="activeTab === 'merge'" />
    </div>
  </div>
</template>
