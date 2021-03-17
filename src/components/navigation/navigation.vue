<template>
  <div class="navigation">
    <h1>My Music</h1>
  </div>  
</template>

<script>
export default {
  props: {
  }
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .navigation {
    display: flex;
    justify-content: center;
    padding: 15px;
    background-color: #44c767;
    color: #ffffff;
  }

  h1 {
    font-size: 3rem;
  }
</style>
