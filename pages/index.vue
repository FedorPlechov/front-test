<template>
  <div class="wrapper">
    <div id="app">
      <TheHeader @sort="sortParameter=$event" />
      <TheMain :sort-parameter="sortParameter" />
    </div>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data () {
    return {
      sortParameter: 'byDefault'
    }
  }
}
</script>
<style lang="scss">
@import "normalize.scss";
@import 'static/style/variables.scss';
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@600&family=Source+Sans+Pro:wght@400;600&display=swap');

* {
  box-sizing: border-box;
}
.wrapper {
  display: flex;
  justify-content: center;
  align-content: center;
  height: 100%;
  width: 100%;
}

#app {
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  background: $background-color;
  font-family: 'Source Sans Pro', sans-serif;
  color: $base-color;
  max-width: 1440px;
  max-height: 900px;
  width: 100%;
  height: 100%;
  padding: 2rem;
  min-width: 393px;
}
</style>
