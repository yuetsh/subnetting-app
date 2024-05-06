<template>
  <n-card :bordered="false" title="工具四：进制转换">
    <n-flex :wrap="false">
      <n-form-item label="点分十进制" label-placement="left">
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
      <n-button @click="calculate1" type="primary">转换</n-button>
    </n-flex>
    <n-flex :wrap="false">
      <n-form-item label="二进制" label-placement="left" label-width="82">
        <n-flex :wrap="false">
          <n-input
            v-model:value="bin.one"
            placeholder=""
            :allow-input="onlyBinary"
          ></n-input>
          <n-input
            v-model:value="bin.two"
            placeholder=""
            :allow-input="onlyBinary"
          ></n-input>
          <n-input
            v-model:value="bin.three"
            placeholder=""
            :allow-input="onlyBinary"
          ></n-input>
          <n-input
            v-model:value="bin.four"
            placeholder=""
            :allow-input="onlyBinary"
          ></n-input>
        </n-flex>
      </n-form-item>
      <n-button @click="calculate2" type="primary">转换</n-button>
    </n-flex>
  </n-card>
</template>
<script lang="ts" setup>
import {
  NButton,
  NCard,
  NFormItem,
  NInput,
  NInputNumber,
  NFlex,
} from "naive-ui"
import { reactive } from "vue"
import {} from "ip-net"

const ip = reactive({
  one: 192,
  two: 168,
  three: 0,
  four: 1,
})

const bin = reactive({
  one: "11000000",
  two: "10101000",
  three: "00000000",
  four: "00000001",
})

function onlyBinary(v: string) {
  return /^[01]{0,8}$/.test(v)
}

function calculate1() {
  bin.one = ip.one.toString(2).padStart(8, "0")
  bin.two = ip.two.toString(2).padStart(8, "0")
  bin.three = ip.three.toString(2).padStart(8, "0")
  bin.four = ip.four.toString(2).padStart(8, "0")
}

function calculate2() {
  ip.one = parseInt(bin.one, 2)
  ip.two = parseInt(bin.two, 2)
  ip.three = parseInt(bin.three, 2)
  ip.four = parseInt(bin.four, 2)
}
</script>
