<template>
  <div class="bgWrapper" />
</template>

<script>
export default {
  name: 'Background',
};
</script>

<style lang="scss" scoped>
  .bgWrapper{
    background-image: url('../assets/heroimage.jpg');
    background-repeat: no-repeat;
    background-size: cover;
    background-position: 80% 0;
    height: 100vh;
    width: 100%;
    position: fixed;
    z-index: -1;

    &::after {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      z-index: 1;
      width: 100%;
      height: 100vh;
      background: rgba(0,0,0,.2);
    }
  }

</style>
