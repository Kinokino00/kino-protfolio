<template>
  <div class="grid gap-4 bg-surface">
    <div class="flex gap-2">
      <!-- <button class="btn-test" @click="changeTheme('default')">預設值</button> -->
      <button class="btn-test" @click="changeTheme('light')">light</button>
      <button class="btn-test" @click="changeTheme('dark')">dark</button>
    </div>

    <div class="grid grid-cols-2 m-3 p-3 bg-primary-100/50 rounded-lg">
      <div
        class="legendPercent"
        v-for="(legend, legendIdx) in item"
        :key="legendIdx"
      >
        <div class="flex items-center gap-2">
          <div class="w-5 h-5 rounded" :class="legend.color"></div>
          <p>{{ legend.title }}</p>
        </div>
        <div class="flex items-baseline gap-1">
          <span class="text-2xl font-bold">{{ Number.isNaN(legend.percent) ? 0 : legend.percent }}</span>%
        </div>
      </div>
    </div>

    <div class="flex gap-1">primary
      <div class="w-20 h-20 bg-primary-50">50</div>
      <div class="w-20 h-20 bg-primary-100">100</div>
      <div class="w-20 h-20 bg-primary-200">200</div>
      <div class="w-20 h-20 bg-primary-300">300</div>
      <div class="w-20 h-20 bg-primary-400">400</div>
      <div class="w-20 h-20 bg-primary-500">500</div>
      <div class="w-20 h-20 bg-primary-600">600</div>
      <div class="w-20 h-20 bg-primary-700">700</div>
      <div class="w-20 h-20 bg-primary-800">800</div>
      <div class="w-20 h-20 bg-primary-900">900</div>
    </div>

    <div class="flex gap-1">secondary
      <div class="w-20 h-20 bg-secondary-50">50</div>
      <div class="w-20 h-20 bg-secondary-100">100</div>
      <div class="w-20 h-20 bg-secondary-200">200</div>
      <div class="w-20 h-20 bg-secondary-300">300</div>
      <div class="w-20 h-20 bg-secondary-400">400</div>
      <div class="w-20 h-20 bg-secondary-500">500</div>
      <div class="w-20 h-20 bg-secondary-600">600</div>
      <div class="w-20 h-20 bg-secondary-700">700</div>
      <div class="w-20 h-20 bg-secondary-800">800</div>
      <div class="w-20 h-20 bg-secondary-900">900</div>
    </div>

    <div class="flex gap-1">tertiary
      <div class="w-20 h-20 bg-tertiary-50">50</div>
      <div class="w-20 h-20 bg-tertiary-100">100</div>
      <div class="w-20 h-20 bg-tertiary-200">200</div>
      <div class="w-20 h-20 bg-tertiary-300">300</div>
      <div class="w-20 h-20 bg-tertiary-400">400</div>
      <div class="w-20 h-20 bg-tertiary-500">500</div>
      <div class="w-20 h-20 bg-tertiary-600">600</div>
      <div class="w-20 h-20 bg-tertiary-700">700</div>
      <div class="w-20 h-20 bg-tertiary-800">800</div>
      <div class="w-20 h-20 bg-tertiary-900">900</div>
    </div>
  </div>
</template>


<script lang="ts" setup>
const changeTheme = (theme: string) => document.querySelector("html")?.setAttribute("data-theme", theme)

const item = [
  { "color": "bg-chart-1", "title": "空調", "percent": null },
  { "color": "bg-chart-2", "title": "222222222222", "percent": null },
  { "color": "bg-chart-3", "title": "Others", "percent": null },
  { "color": "bg-chart-4", "title": "照明", "percent": null },
  { "color": "bg-chart-5", "title": "插座", "percent": null },
  { "color": "bg-chart-6", "title": "22", "percent": null }
]
</script>


<style lang="scss" scoped>
.btn-test {
  @apply bg-primary-800 dark:border-secondary-300;
}
</style>
