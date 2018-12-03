<template>
  <div id="level">
    <ul>
      <li :class="{ 'active-step': step == 1 }"></li>
      <li :class="{ 'active-step': step == 2 }"></li>
      <li :class="{ 'active-step': step == 3 }"></li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "level",
  props: {
    step: Number
  },
  created() {}
};
</script>

<style scoped>
ul {
  list-style: none;
  display: flex;
  justify-content: center;
}
#level ul li {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: white;
  transition: 0.3s ease;
  margin: 5px;
}
#level ul li.active-step {
  background: pink;
}
</style>
