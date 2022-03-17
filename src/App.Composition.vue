// Part 9. Vue.js -- Ch3 컴포지션 API -- 1. 개요
<!--
<template>
  <h1 @click="increase">
    {{ count }} / {{ doubleCount }}
  </h1>
  <h1>
    {{ message }} / {{ reversedMessage }}
  </h1>
</template>

<script>
import { ref, computed } from 'vue'

export default {
  setup() {
    const message = ref('Hello World!')
    const reversedMessage = computed(() => {
      return message.value.split('').reverse.join('')
    })

    const count = ref(0)
    const doubleCount = computed(() => count.value * 2)
    function increase() {
      count.value += 1
    }

    return {
      message,
      reversedMessage,
      count,
      doubleCount,
      increase
    }
  } 
}
</script>
-->

// Part 9. Vue.js -- Ch3 컴포지션 API -- 3. 기본 옵션과 라이프사이클
<!--
<template>
  <h1 @click="increase">
    {{ count }}
  </h1>
  <h1 @click="changeMessage">
    {{ message }}
  </h1>
</template>

<script>
import { ref, computed, watch, onMounted } from 'vue'   // mounted -> onMounted

export default {
  setup() {   // setup은 created 직후에 실행되기 때문에 created()는 따로 import할 필요가 없음
    const count = ref(0)
    const doubleCount = computed(() => {
      return count.value * 2
    })
    function increase() {
      count.value += 1
    }

    const message = ref('Hello World')
    const reversedMessage = computed(() => {
      return message.value.split('').reverse().join('')
    })
    watch(message, (newValue) => {  // 매개변수 1개면 () 생략 가능 > newValue => {~~}
      console.log(newValue)
    })
    function changeMessage() {
      message.value = 'Good~!'
    }
    console.log(message.value)  // 이게 created()에서 사용된 함수와 같은

    onMounted(() => {
      console.log(count.value)
    })

    return {
      count,
      doubleCount,
      increase,
      message,
      reversedMessage,
      changeMessage
    }
  }
}
</script>
-->

// Part 9. Vue.js -- Ch3 컴포지션 API -- 4. props, context