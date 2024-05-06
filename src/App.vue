<template>
  <n-config-provider :locale="zhCN" :date-locale="dateZhCN">
    <n-tabs type="segment">
      <n-tab-pane name="子网划分" display-directive="show">
        <Subnetting />
      </n-tab-pane>
      <n-tab-pane name="子网掩码" display-directive="show">
        <Netmask />
        <n-divider style="margin: 0" />
        <Host />
      </n-tab-pane>
      <n-tab-pane name="进制转换" display-directive="show">
        <binary />
      </n-tab-pane>
    </n-tabs>
  </n-config-provider>
</template>
<script setup lang="ts">
import {
  zhCN,
  dateZhCN,
  NConfigProvider,
  NTabs,
  NTabPane,
  NDivider,
} from "naive-ui"
import Subnetting from "./Subnetting.vue"
import Netmask from "./Netmask.vue"
import Host from "./Host.vue"
import Binary from "./Binary.vue"
</script>
<style scoped></style>
