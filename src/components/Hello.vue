// Part 9. Vue.js -- Ch2 -- 20. 컴포넌트 - Refs
<template>
  <h1>Hello~</h1>
  <h1 ref="good">
    Good!
  </h1>
</template>

// refs는 최상위 엘리먼트만 접근 가능하다, 최상위가 여러개라면 $el로 어떤걸 접근해야하는지 모름