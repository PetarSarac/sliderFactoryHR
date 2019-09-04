<template>
  <div id="app">
    <div class="header"></div>
    <div class="header-2">
      <div class="header-2__content">Skup drugih elemenata na stranici</div>
    </div>
    <Slider/>
    <div class="footer">
      <div class="footer__content">Skup drugih elemenata na stranici</div>
    </div>
  </div>
</template>

<script>
import Slider from './components/Slider.vue'

export default {
  name: 'app',
  components: {
    Slider
  }
}
</script>

<style lang="scss">
//Basic stuff
body {
  margin: 0 ;
  font-family: "Source Sans Pro";
}
#app {
  display: grid;
  grid-template-columns: repeat(12,1fr);
  grid-auto-rows: minmax(100px,auto);
  grid-column-gap: 20px;
  margin: 0 auto;
  max-width: 1140px;
}

.header{
  background-color: lighten(gray,30%);
  grid-column: 1 / 5;
  grid-row: 1 / span 2;
  border-radius: 0 0 5px 5px;

  &-2 {
    display: flex;
    background-color: lighten(gray,30%);
    grid-column: 5 / 13;
    grid-row: 1 / span 2;
    border-radius: 0 0 5px 5px;

    &__content {
      color: white;
      font-size: 24px;
      padding-left: 170px;
      align-self: center;
    }
  }
}

.footer {
  display: flex;
  background-color:lighten(gray,30%);
  grid-column: 1 / 13;
  grid-row:  9 / span 2;
  border-radius: 5px 5px 0 0;

  &__content {
    color: white;
    font-size: 24px;
    padding-left: 170px;
    align-self: center;
  }
}
</style>
