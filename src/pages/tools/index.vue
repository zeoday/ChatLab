<script setup lang="ts">
import { ref } from 'vue'
import { SubTabs } from '@/components/UI'
import MergeTab from './components/MergeTab.vue'
import PageHeader from '@/components/layout/PageHeader.vue'

// Tab 配置
const tabs = [{ id: 'merge', label: '合并聊天记录', icon: 'i-heroicons-document-duplicate' }]

const activeTab = ref('merge')
</script>

<template>
  <div class="flex h-full flex-col bg-gray-50 dark:bg-gray-950">
    <!-- Header -->
    <PageHeader title="实用工具" description="提供聊天记录处理的实用工具" icon="i-heroicons-wrench-screwdriver" />

    <!-- Tabs -->
    <SubTabs v-model="activeTab" :items="tabs" persist-key="toolTab" />

    <!-- Tab Content -->
    <div class="flex-1 overflow-auto p-6">
      <MergeTab v-if="activeTab === 'merge'" />
    </div>
  </div>
</template>
