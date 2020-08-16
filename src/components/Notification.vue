<template>
  <div class="notification-container">
    <p>You have already entered this letter</p>
  </div>
</template>

<script>
export default {};
</script>

<style>
.notification-container {
  background-color: rgba(0, 0, 0, 0.3);
  border-radius: 10px 10px 0 0;
  padding: 15px 20px;
  position: absolute;
  bottom: -50px;
  transition: transform 0.3s ease-in-out;
  transform: translateY(-450px);
}

.notification-container p {
  margin: 0;
}
</style>