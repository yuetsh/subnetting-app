<template>
  <n-card :bordered="false" title="工具三：通过主机数计算子网掩码">
    <n-flex>
      <n-form-item label="需要的主机数" label-placement="left">
        <n-input-number
          v-model:value="host"
          min="0"
          max="4294967294"
          placeholder=""
          :show-button="false"
        ></n-input-number>
      </n-form-item>
      <n-button @click="calculate" type="primary">计算</n-button>
      <n-button @click="clear">清空</n-button>
    </n-flex>
    <div vertical>
      <n-h3>掩码长度：{{ maskLen }}</n-h3>
      <n-h3>子网掩码：{{ netmask }}</n-h3>
      <n-h3>可用主机数：{{ size }}</n-h3>
    </div>
  </n-card>
</template>

<script lang="ts" setup>
import { toMask } from "ip-net/src/toMask"
import { NButton, NCard, NFormItem, NInputNumber, NFlex, NH3 } from "naive-ui"
import { ref } from "vue"

const host = ref(100)
const maskLen = ref(25)
const netmask = ref("255.255.255.128")
const size = ref(126)

function calculate() {
  const hostLen = Math.ceil(Math.log(host.value + 2) / Math.log(2))
  maskLen.value = 32 - hostLen
  netmask.value = toMask(maskLen.value)
  size.value = Math.pow(2, hostLen) - 2
}

function clear() {
  host.value = 100
  maskLen.value = 25
  netmask.value = "255.255.255.128"
  size.value = 126
}
</script>
