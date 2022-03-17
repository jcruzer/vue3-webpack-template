// Part 9. Vue.js -- Ch2 -- 15. 컴포넌트 - 기초
<!--
<template>
  <MyBtn text="Banana" />
  <MyBtn :color="color">
    Apple
  </MyBtn>
  <MyBtn
    large
    :color="color">
    Cherry
  </MyBtn>
  <MyBtn>
    <span style="color: red;">Banana</span><MyBtn />
  </mybtn>
</template>

<script>
// component의 장점은 한번 만들어두면 재활용 가능
// 부모의 정보를 자식에게 보내줄때 props 사용
import MyBtn from '~/components/MyBtn'

export default {
  components: {
    MyBtn
  },
  data() {
    return {
      color: '#000'
    }
  }
}
</script>
-->
// Part 9. Vue.js -- Ch2 -- 16. 컴포넌트 - 속성 상속
<!--
<template>
  <MyBtn
    class="mandue"
    style="color: red;"
    title="Hello World">
    Banana
  </MyBtn>
</template>

<script>
import MyBtn from '~/components/MyBtn'

export default {
  components: {
    MyBtn
  }  
}
</script>
-->
// Part 9. Vue.js -- Ch2 -- 17. 컴포넌트 - Eimit
<!--
<template>
  <MyBtn
    @mandue="log"
    @change-msg="logMsg">
    Banana
  </MyBtn>
</template>
// vue에선 대시케이스 -
// javascript에선 카멜케이스

<script>
import MyBtn from '~/components/MyBtn'

export default {
  components: {
    MyBtn
  },
  methods: {
    log(event) {
      console.log("click~")
      console.log(event)
    },
    logMsg(msg) {
      console.log(msg)
    }
  }
}
</script>
-->

// Part 9. Vue.js -- Ch2 -- 18. 컴포넌트 - Slot
<!--
<template>
  <MyBtn>
    <template #icon>
      <span>(B)</span>
    </template>
    <template #text>
      <span>Banana</span>
    </template>
  </MyBtn>
</template>

// v-bind: > :
// v-on: > @
// v-slot > #

<script>
import MyBtn from '~/components/MyBtn'

export default {
  components: {
    MyBtn
  }
}
</script>
-->

// Part 9. Vue.js -- Ch2 -- 19. 컴포넌트 - Inject
// 부모 -> 자식 -> 자식으로 내려가는데 중간에 쓸모없이 정의들이 필요함
// provide를 이용하면 됨
<!--
<template>
  <button @click="message = 'good'">
    Click
  </button>
  <h1>App: {{ message }}</h1>
  <Parent />
</template>
//<Parent :msg="message" />

<script>
import Parent from '~/components/Parent'
import { computed } from 'vue'

export default {
  components: {
    Parent
  },
  data() {
    return {
       message: 'Hello World~'
    }
  },
  // provide를 사용하면 반응성 제공 X(업데이트 안됨), 데이터를 주는용도로 적합함
  // 반응성을 유지해주려면 computed() 함수를 이용하기, 적용되는 자식에는 .value 붙여줘야 원하는 값 나옴
  // 콜백함수 () => { return ~~ } : 리턴값만 있을때는 () => ~~ 수정가능
  provide() {
    return {
      //msg: this.message
      // msg: computed(() => {
      //   return this.message
      // })
      msg: computed(() => this.message)
    }
  }
}
</script>
-->

// Part 9. Vue.js -- Ch2 -- 20. 컴포넌트 - Refs
<template>
  <h1 ref="hello">
    Hello World!
  </h1>
  <Hello ref="hello" />
</template>

// ref는 html과 연결된 직후(mounted된 이후에) 사용 가능함, created에선 사용 불가능

<script>
import Hello from '~/components/Hello'
export default {
  components: {
    Hello
  },
  // refs를 이용해 참조할 경우 this.$refs.ref이름.$el을 써야 원하는 엘리먼트 사용 가능
  // refs는 최상위 엘리먼트만 접근 가능하다, 최상위가 여러개라면 $el로 어떤걸 접근해야하는지 모름
  // 그럴땐 또 refs 써서 최상위 엘리먼츠중 원하는 요소에 refs값 명시
  mounted() {
    console.log(this.$refs.hello.$el)
    console.log(this.$refs.hello.$refs.good)
  }
}
</script>