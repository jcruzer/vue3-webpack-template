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
export default {
  data() {
    return {
      message: 'Hello World!',
      count: 0
    }
  },
  computed: {
    doubleCount() {
      return this.count * 2
    },
    reversedMessage() {
      return this.message.split('').reverse().join('')
    }
  },
  methods: {
    increase() {
      this.count += 1
    }
  }
}
</script>
-->

// Part 9. Vue.js -- Ch3 컴포지션 API -- 2. 반응형 데이터(반응성)
<!--
<template>
  <div @click="increase">
    {{ count }}
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  /*
  data() {
    return {
      count: 0
    }
  },
  methods: {
    increase() {
      this.count += 1
    }
  },
  // 위의 코딩은 반응성이 있음, 카운트업 잘됨
  */

  // 아래함수는 아직 반응성이 없음, 카운트업 되지만 디스플레이는 안바뀜
  // ref 함수를 사용해서 반응성을 갖게하지만, 객체데이터가 반환이 되서 하나의 데이터로 직접사용 불가
  // .value를 이용해서 데이터에 접근해 사용
  
  setup() {
    let count = ref(0)
    function increase() {
      count.value += 1
    }
    
    // return으로 반환하고나서는 .value 안붙이고 그대로 사용해도 됨
    return {
      count,
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
    {{ count }} / {{ doubleCount }}
  </h1>
  <h1 @click="changeMessage">
    {{ message }} / {{ reversedMessage }}
  </h1>
</template>

<script>
export default {
  data() {
    return {
      count: 0,
      message: 'Hello World!'
    }
  },
  computed: {
    doubleCount() {
      return this.count * 2
    },
    reversedMessage() {
      return this.message.split('').reverse().join('')
    }
  },
  watch: {
    message(newValue) {
      console.log(newValue)
    }
  },
  created() {
    console.log(this.message)
  },
  mounted() {
    console.log(this.count)
  },
  methods: {
    increase() {
      this.count += 1
    },
    changeMessage() {
      this.message = 'Good~'
    }
  }
}
</script>
-->
// Part 9. Vue.js -- Ch3 컴포지션 API -- 4. props, context

<template>
  <MyBtn
    class="mandue"
    style="color: red;"
    color="#ff0000"
    @hello="log">
    Apple
  </MyBtn>
</template>

<script>
import MyBtn from '~/components/MyBtn'

export default {
  components: {
    MyBtn
  },
  methods: {
    log() {
      console.log('Hello World')
    }
  }
}
</script>