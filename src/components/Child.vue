// Part 9. Vue.js -- Ch2 -- 19. 컴포넌트 - Inject
<template>
  <div>
    Child: {{ msg.value }}
  </div>
</template>
// computed를 사용해서 원하는 결과를 뽑아내려면 msg.value 써야함

<script>
export default {
  inject: ['msg']
}
</script>