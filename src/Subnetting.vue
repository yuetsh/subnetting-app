<template>
  <n-card :bordered="false" title="工具一：请填写 IPv4 地址和掩码长度">
    <n-flex :wrap="false">
      <n-form-item label="IP地址" label-placement="left">
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
      <n-form-item label="掩码长度" label-placement="left">
        <n-input-number
          v-model:value="ip.netmask"
          min="0"
          max="32"
          placeholder=""
          :show-button="false"
        ></n-input-number>
      </n-form-item>
    </n-flex>
    <n-flex justify="center">
      <n-button @click="calculate" type="primary">计算</n-button>
      <n-button @click="clear">清空</n-button>
    </n-flex>
    <div v-if="show">
      <n-h3>可用地址数量：{{ addressCount }}</n-h3>
      <n-h3>子网掩码：{{ mask }}</n-h3>
      <n-h3>网络地址：{{ networkAddress }}</n-h3>
      <n-h3>主机范围：{{ first }} - {{ last }}</n-h3>
      <n-h3>广播地址：{{ broadcastAddress }}</n-h3>
    </div>
  </n-card>
</template>
<script setup lang="ts">
import { ref, computed, reactive } from "vue"
import { NButton, NCard, NFormItem, NInputNumber, NFlex, NH3 } from "naive-ui"
import { subnet } from "ip-net"

const ip = reactive({
  one: 192,
  two: 168,
  three: 0,
  four: 1,
  netmask: 24,
})

const ipStr = computed(() => `${ip.one}.${ip.two}.${ip.three}.${ip.four}`)

const show = ref(false)
const addressCount = ref(0)
const mask = ref("")
const networkAddress = ref("")
const broadcastAddress = ref("")
const first = ref("")
const last = ref("")

function calculate() {
  const sub = subnet(`${ipStr.value}/${ip.netmask}`)

  show.value = true
  addressCount.value = sub.addressCount
  mask.value = sub.mask
  networkAddress.value = sub.networkAddress
  broadcastAddress.value = sub.broadcastAddress
  first.value = sub.getFirstHost()?.address ?? ""
  last.value = sub.getLastHost()?.address ?? ""
}

function clear() {
  show.value = false
  ip.one = 192
  ip.two = 168
  ip.three = 0
  ip.four = 1
  ip.netmask = 24
}
</script>
