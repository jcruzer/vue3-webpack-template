// Part 9. Vue.js -- Ch2 -- 05. Getter, Setter
<!--
<template>
  <button @click="add">
    ADD
  </button>
  <h1>{{ reversedMessage }}</h1>
  <h1>{{ reversedMessage }}</h1>
  <h1>{{ reversedMessage }}</h1>
  <h1>{{ reversedMessage }}</h1>
</template>

<script>
export default {
  data() {
    return {
      // Getter, Setter
      msg: 'Hello Coputed!!'
    }
  },
  computed: {   // 캐싱 기능이 있어서 한번만 연산하고 이후엔 안함, 반복사용되는 데이터들에 많이 사용, 읽기전용(쓰기 불가)
  // Getter
    // reversedMessage() {
    //   return this.msg.split('').reverse().join('')
    // }
    reversedMessage: {
      get() {
        return this.msg.split('').reverse().join('')
      },
      set(newValue) {
        this.msg = newValue
      }
    }
  },
  methods: {
    add() {
      this.reversedMessage += '?!'
    }
  }
}
</script>
-->

// Part 9. Vue.js -- Ch2 -- 06. Watch
<!--
<template>
  <h1 @click="changeMessage">
    {{ msg }}
  </h1>
  <h1>{{ reversedMessage }}</h1>
</template>

<script>
export default {
  data() {
    return {
      msg: 'Hello?'
    }
  },
  computed: {
    reversedMessage() {
      return this.msg.split('').reverse().join('')
    }
  },
  watch: {  // 데이터를 감시하다 변경되면 실행
  // computed 데이터도 사용 가능
    msg: function() {   // [: function] 생략 가능 -> msg() {}
      console.log('msg: ', this.msg)
    },
    reversedMessage() {
      console.log('reversedMessage: ', this.reversedMessage)
    }
  },
  methods: {
    changeMessage() {
      this.msg = 'Good!'
    }
  }
}
</script>
-->

// Part 9. Vue.js -- Ch2 -- 07. 클래스와 스타일 바인딩
<!--
<template>
  <h1 
    :class="{ active: isActive }"
    @click="activate">
    Hello?!({{ isActive }})
  </h1>
</template>

<script>
export default {
  data() {
    return {
      isActive: false
    }
  },
  methods: {
    activate() {
      this.isActive = true
    }
  }
}
</script>

<style scoped>
  .active {
    color: red;
    font-weight: bold;
  }
</style>
-->
<!--
<template>
  <h1
    :style="
      //color: color,
      //fontSize: fontSize
      //color, fontSize
      // 이렇게 객체데이터에서 속성의 이름과 데이터의 이름이 같으면 단축 가능
      [fontStyle, backgroundStyle]
    "
    @click="changeStyle">
    Hello?!
  </h1>
</template>

<script>
export default {
  data() {
    return {
      // 이런식으로 데이터 하나하나로 쓸수 있지만
      color: 'orange',
      fontSize: '30px',
      // 객체데이터로 만들수도(이게 관리하기 편할듯)
      fontStyle: {
        color: 'orange',
        fontSize: '30px'
      },
      backgroundStyle: {
        backgroundColor: 'black'
      }
    }
  },
  methods: {
    changeStyle() {
      this.fontStyle.color = 'red'
      this.fontStyle.fontSize = '50px'
    }
  }
}
</script>
-->

// Part 9. Vue.js -- Ch2 -- 08. 조건부 렌더링
<!--
<template>
  <button @click="handler">
    Click me!
  </button>
  <h1 v-if="isShow">
    Hello?!
  </h1>
</template>
// template로 태그들을 감싸면 래퍼역할만하고 최종 렌더링결과(html)에는 엘리먼트(태그)가 포함되지 않음
// v-show는 엘리먼트는 포함하지만 렌더링화면에는 표시되지않음(display:none)
<script>
export default {
  data() {
    return {
      isShow: false,
      count: 0
    }
  },
  methods: {
    handler() {
      this.isShow = !this.isShow
      this.count += 1
    }
  }
}
</script>
-->
// Part 9. Vue.js -- Ch2 -- 09. 리스트 렌더링
<!--
<template>
  <button @click="handler">
    Click me!
  </button>
  <ul>
    <li
      v-for="(fruit, index) in newFruits"
      :key="fruit.id">
      {{ fruit.name }} - {{ index + 1 }} - {{ fruit.id }}
    </li>
    // fruit라는 객체를 객체구조분해를 하면 아래처럼
    <li
      v-for="({ id, name }, index) in newFruits"
      :key="id">
      {{ name }} - {{ index + 1 }} - {{ id }}
    </li>
  </ul>
</template>

<script>
// v-for문에서는 v-bind:key="고유한값"이 필요한데 고유한 값을 쉽게 만들어주기 위해서 shortid를 설치(npm i -D shortid)
import shortid from 'shortid'
export default {
  data() {
    return {
      fruits: ['Apple', 'Banana', 'Cherry']
    }
  },
  computed: {
    newFruits() {
      return this.fruits.map(fruit => ({
        // return {
          id: shortid.generate(),
          name: fruit
        // }
        // 실행문이 한개만 리턴될경우 return {} 생략 가능
      }))
    }
  },
  methods: {
    handler() {
      this.fruits.push('Orange')
    }
  }
}
</script>
-->

// Part 9. Vue.js -- Ch2 -- 10. 이벤트 핸들링
<!--
<template>
  <button @click="handler('hi', $event)">
    Click 1
  </button>
  <button @click="handler('bye', $event)">
    Click 2
  </button>
</template>
// 해당 event를 지정할땐 $이벤트명

<script>
export default {
  methods: {
    // event라는 매개변수는 해당이벤트의 객체정보들 위의 함수에선 click이라는 이벤트
    // handler(e) {
    //   console.log(e)
    //   console.log(e.target.textContent)
    // }
      handler(msg, event) {
        console.log(msg)
        console.log(event)
      }
  }
}
</script>
-->
<!--
<template>
  <button @click="handlerA(), handlerB()">
    click me!
  </button>
</template>
// 여러개의 메소드를 실행시킬땐 매개변수가 없더라도 () 써줘야함
<script>
export default {
  methods: {
    handlerA() {
      console.log('A')
    },
    handlerB() {
      console.log('B')
    }
  }
}
</script>
-->

// Part 9. Vue.js -- Ch2 -- 11. 이벤트 핸들링 - 이벤트 수식어
<!--
<template>
  <a
    href="https://naver.com"
    target="_blank"
    @click.once="handler">
    Naver
  </a>
</template>

<script>
export default {
  methods: {
    handler() {
      console.log('ABC!')
    }
  }
}
</script>
-->
<!--
<template>
  <div
    class="parent"
    @click.self="handlerA">
    <div
      class="child">
    </div>
  </div>
</template>
// 이벤트 버블링이 일어나면서 자식을 눌러도 부모를 누른 효과
// vue에서 .stop은 script에서 .stopPropagation

// 이벤트 캡쳐링이 일어나면서 부모를 눌러도 자식에게 효과가 적용(.capture)
// .self는 자식을 제외한 부모영역 지정

<script>
export default {
  methods: {
    handlerA(event) {
      console.log('A')
      console.log(event.target)   // target은 눌려진 영역
      console.log(event.currentTarget)    // 동작이 실행된 영역
    },
    handlerB() {
      //event.stopPropagation()
      // stopPropagation사용하면 이벤트 버블링 방지
      console.log('B')

    },
  }
}
</script>

<style scoped lang="scss">
  .parent {
    width: 200px;
    height: 100px;
    background-color: royalblue;
    margin: 10px;
    padding: 10px;
    .child {
      width: 100px;
      height: 100px;
      background-color: orange;
    }
  }
</style>
-->
<!--
<template>
  <div
    class="parent"
    @wheel.passive="handler">
    <div
      class="child">
    </div>
  </div>
</template>
// passive를 붙이면 화면과 동작을 분리? 더 쾌적한 환경 적용

<script>
export default {
  methods: {
    handler(event) {
      for (let i = 0 ; i < 10000; i += 1){
        console.log(event)
      }
    }
  }
}
</script>

<style scoped lang="scss">
  .parent {
    width: 200px;
    height: 100px;
    background-color: royalblue;
    margin: 10px;
    padding: 10px;
    overflow: auto;
    .child {
      width: 100px;
      height: 2000px;
      background-color: orange;
    }
  }
</style>
-->

// Part 9. Vue.js -- Ch2 -- 12. 이벤트 핸들링 - 키 수식어
<!--
<template>
  <input
    type="text"
    @keydown.ctrl.enter="handler" />
</template>

<script>
export default {
  methods: {
    handler() {
    //handler(event) {
      // if (event.key == "Enter")   // 이걸 편하게 쓰는게 @keydown.키이름(케밥케이스 - )
      console.log("Enter~~!")
    }
  }
}
</script>
-->

// Part 9. Vue.js -- Ch2 -- 13. 폼 입력 바인딩
<!--
<template>
  <h1>{{ msg }}</h1>
  <input
    type="text"
    v-model="msg" />
  <h1>{{ checked }}</h1>
  <input
    type="checkbox"
    v-model="checked" />
</template>
//     :value="msg"
//     @input="msg = $event.target.value" />
// 이 두개를 v-model="msg" 이걸로 합칠 수 있음
// 한글을 입력할땐 위에 value + input을 사용하는게 나음(한박자 느리게 반응)

<script>
export default {
  data() {
    return {
      msg: "Hello World",
      checked: false
    }
  },
  // methods: {
  //   handler(event) {
  //     console.log(event.target.value)
  //     this.msg = event.target.value   // 이런식으로 양방향 데이터 바인딩
  //   }
  // }
}
</script>
-->

// Part 9. Vue.js -- Ch2 -- 14. v-model 수식어
<!--
<template>
  <h1>{{ msg }}</h1>
  <input
    type="text"
    v-model.trim="msg" />
</template>
// change는 값이 바뀌고 나서 갱신(포커스가 해제되었을때)
//    :value="msg"
//    @change="msg = $event.target.value" />
// 위의 두개를 v-model.lazy로 합쳐서 쓸 수 있음

// v-model.number를 쓰면 string이 아니라 number로 타입이 유지
// v-model.trim을 쓰면 공백제거
<script>
export default {
  data() {
    return {
      msg: "Hello World"
    }
  },
  watch: {
    msg() {
      console.log(this.msg.trim())
    }
  }
}
</script>
-->