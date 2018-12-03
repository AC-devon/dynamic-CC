<template>
  <div id="pay-btn">
    <div id="pay">PAY $45.00</div>
  </div>
</template>

<script>
export default {};
</script>

<style>
#pay-btn {
  width: 100%;
  height: 50px;
  background: black;
  color: white;
  position: absolute;
  left: 0;
  right: 0;
  bottom: -500px;
  transition: all 0.5s ease;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
}
</style>
