<template>
  <n-card :bordered="false" title="工具二：不同格式的子网掩码的转换">
    <n-flex>
      <n-form-item label="掩码长度" label-placement="left">
        <n-input-number
          v-model:value="ip.netmask"
          min="0"
          max="32"
          placeholder=""
          :show-button="false"
        ></n-input-number>
      </n-form-item>
      <n-button @click="calculate1" type="primary">转换</n-button>
      <n-button @click="clear">清空</n-button>
    </n-flex>
    <n-flex :wrap="false">
      <n-form-item label="子网掩码" label-placement="left">
        <n-flex :wrap="false">
          <n-input-number
            v-model:value="ip.one"
            min="0"
            max="255"
            placeholder=""
            :show-button="false"
          ></n-input-number>
          <n-input-number
            v-model:value="ip.two"
            min="0"
            max="255"
            placeholder=""
            :show-button="false"
          ></n-input-number>
          <n-input-number
            v-model:value="ip.three"
            min="0"
            max="255"
            placeholder=""
            :show-button="false"
          ></n-input-number>
          <n-input-number
            v-model:value="ip.four"
            min="0"
            max="255"
            placeholder=""
            :show-button="false"
          ></n-input-number>
        </n-flex>
      </n-form-item>
      <n-button @click="calculate2" type="primary">转换</n-button>
      <n-button @click="clear">清空</n-button>
    </n-flex>
    <n-text>{{ label }}</n-text>
  </n-card>
</template>

<script lang="ts" setup>
import { ipv4ToMask } from "ip-net/src/toMask"
import { toMaskLen } from "ip-net/src/toMaskLen"
import { NButton, NCard, NFormItem, NInputNumber, NFlex, NText } from "naive-ui"
import { computed, reactive, ref } from "vue"

const ip = reactive({
  one: 255,
  two: 255,
  three: 255,
  four: 0,
  netmask: 24,
})

const size = ref(254)
const label = computed(() => {
  if (size.value < 0) return "可用地址数量：出错，总共地址数量：出错"
  return `可用地址数量：${size.value}，总共地址数量：${size.value + 2}`
})

function calculate1() {
  const mask = ipv4ToMask(ip.netmask)
  ip.one = parseInt(mask.split(".")[0])
  ip.two = parseInt(mask.split(".")[1])
  ip.three = parseInt(mask.split(".")[2])
  ip.four = parseInt(mask.split(".")[3])
  size.value = Math.pow(2, 32 - ip.netmask) - 2
}

function calculate2() {
  const mask = `${ip.one}.${ip.two}.${ip.three}.${ip.four}`
  const len = toMaskLen(mask)
  ip.netmask = len
  calculate1()
}

function clear() {
  ip.one = 255
  ip.two = 255
  ip.three = 255
  ip.four = 0
  ip.netmask = 24
  size.value = 254
}
</script>
