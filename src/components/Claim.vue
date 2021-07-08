<template>
  <div class="claimWrapper">
    <h1 class="claim">Spacer</h1>
    <p class="subclaim">Begin your journey through our amazing galaxy </p>
    <p class="subclaim">Type the object you want to find</p>
  </div>
</template>

<script>
export default {
  name: 'Claim',
};
</script>

<style lang="scss" scoped>
  .claimWrapper{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    text-align: center;

    .claim{
      font-size: 50px;
      margin: 0;

      @media (min-width: 768px) {
        font-size: 80px;
      }
      @media (min-width: 900px) {
        font-size: 100px;
      }
    }
    .subclaim{
      margin: 25px 0 0 0;
      font-size: 15px;
      font-weight: 400;

      @media (min-width: 768px) {
        font-size: 17px;
        width: 500px;
        letter-spacing: 1px;
        font-weight: 400;
        line-height: 1;
      }
    }
  }
</style>
