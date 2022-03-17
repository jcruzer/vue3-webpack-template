// Part 9. Vue.js -- Ch2 -- 15. 컴포넌트 - 기초
<!--
<template>
  <div 
    :class="{ large }"
    :style="{ backgroundColor: color }"
    class="btn">
    <slot></slot>
  </div>
</template>
// v-bind:style=" {~~~} "로 사용 가능
// :class="{ large: large }" 속성과 데이터값이 같으면 데이터부분 생략 가능
// componenets들도 열린태그 닫힌태그처럼 사용 가능  <slot></slot> 이용해서 그 내용이 어디에 출력되는지 위치지정

// props를 이용해 부모 - 자식 간 데이터 통신 가능
<script>
export default {
  props: {    // 재사용할때 조정 가능한 속성들
    color: {  // color 속성 사용 가능, 기본적으로 타입과 값을 초기화
      type: String,
      default: 'gray'
    },
    large: {
      type: Boolean,
      default: false
    },
    text: {
      type: String,
      default: ""
    }
  }
}
</script>

<style scoped lang="scss">
  .btn {
    display: inline-block;
    margin: 4px;
    padding: 6px 12px;
    border-radius: 4px;
    background-color: gray;
    color:white;
    cursor: pointer;
    &.large {
    font-size: 20px;
    padding: 10px 20px;
    }
  }
</style>
-->
// Part 9. Vue.js -- Ch2 -- 16. 컴포넌트 - 속성 상속
<!--
<template>
  
  <div class="btn">
    <slot></slot>
  </div>
  <h1 v-bind="$attrs"></h1>

</template>
// 최상위요소가 2개 이상일때는 componenet에 속성적용이 안된다(상속불가)

// <h1
//    :class="$attrs.class"
//    :style="$attrs.style"></h1> 이거를
//    <h1 v-vind="$attrs"></h1> 이렇게 줄일 수있음(모든 속성 상속)
// $attrs 객체로 부모의 속성 접근해서 class 따옴

<script>
export default {
  inheritAttrs: false,   // 속성의 상속을 안함(최상위요소가 있어도)
  created() {   // components가 생성된 직후
    console.log(this.$attrs)
  }
}
</script>

<style scoped>
  .btn {
    display: inline-block;
    margin: 4px;
    padding: 6px 12px;
    border-radius: 4px;
    background-color: gray;
    color:white;
    cursor: pointer;
  }
</style>
-->
// Part 9. Vue.js -- Ch2 -- 17. 컴포넌트 - Eimit
<!--
<template>
  <div class="btn">
    <slot></slot>
  </div>
  <h1 @dblclick="$emit('mandue', $event)">
    abc
  </h1>
  <input
    type="text"
    v-model="msg" />
</template>

<script>
export default {
  emits: [    // 부모에서 정의된 이벤트를 컴포넌트 내부에서 상속받아 사용할것이라고 정의
    'mandue',
    'changeMsg'
  ],
  data() {
    return {
      msg: ''
    }
  },
  watch: {
    msg() {
      this.$emit('changeMsg', this.msg)
    }
  }
}
</script>

<style scoped>
  .btn {
    display: inline-block;
    margin: 4px;
    padding: 6px 12px;
    border-radius: 4px;
    background-color: gray;
    color:white;
    cursor: pointer;
  }
</style>
-->

// Part 9. Vue.js -- Ch2 -- 18. 컴포넌트 - Slot
<!--
<template>
  <div class="btn">
    <slot name="icon"></slot>
    <slot name="text"></slot>
  </div>
</template>
// 콘탠트(내용)이 없으면 slot의 내용이 출력됨, 내용이 있다면 부모요소에 있는 콘탠트가 출력(Fallback Contents)
// 슬롯의 순서를 저런식으로 name을 지정해서 설정할 수 있음


<style scoped>
  .btn {
    display: inline-block;
    margin: 4px;
    padding: 6px 12px;
    border-radius: 4px;
    background-color: gray;
    color:white;
    cursor: pointer;
  }
</style>
-->

// Part 9. Vue.js -- Ch2 -- 19. 컴포넌트 - Inject