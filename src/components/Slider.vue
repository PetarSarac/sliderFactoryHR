<template>
  <div class="slider">
        <transition-group 
          :name="transitionName"
          class="slider--1" 
          tag="div"
          >
            <div
              v-for="sliderPhoto in sliderPhotos.slice(0,6)"
              :key="sliderPhoto.url"
              class="slider__photo">
                <img :src="require('@/assets/' + sliderPhoto.url)" alt="Slide img">
            </div>
        </transition-group>
      
        <transition-group 
          :name="transitionName"
          tag="div" 
          class="slider--2"
          >
            <div 
              v-for="sliderPhoto in sliderPhotos.slice(6)"
              :key="sliderPhoto.url"
              class="slider__photo">
                <img :src="require('@/assets/' + sliderPhoto.url)" alt="Slide img">
            </div>
          
        </transition-group>
       
        

    <div class="slider__controls">
        <button class="slider__controls--prev" @click="prev" :disabled="disabled">
          <img src="@/assets/arrow-blue-left.png" alt="Controls left">
        </button>
        <button class="slider__controls--next" @click="next" :disabled="disabled">
          <img src="@/assets/arrow-blue-right.png" alt="Controls right">
        </button>
    </div>

    <div class="slider__text">
      <h2>Lorem ipsum dolor sit amet consectetuer adipiscing elit</h2>
      <p>Ut wisi enim ad minim veniam, quis nostrud exerci tation ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat.    Duis autem vel eum iriure dolor in hendrerit in vulputate velit esse molestie consequat.
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Slider',
  data(){
    return {
      sliderPhotos: [
        {url: 'slider-image-1.jpg'},
        {url: 'slider-image-2.jpg'},
        {url: 'slider-image-3.jpg'},
        {url: 'slider-image-4.jpg'},
        {url: 'slider-image-5.jpg'},
        {url: 'slider-image-6.jpg'},
        {url: 'slider-image-7.jpg'},
        {url: 'slider-image-8.jpg'},
        {url: 'slider-image-9.jpg'},
        {url: 'slider-image-10.jpg'},
        {url: 'slider-image-11.jpg'}    
      ],
      transitionName: 'next',
      disabled: false
    }
  },
  methods: {
    
    next(){
      this.disabled = true; // Disable button while transition is active
      this.transitionName = 'next' // Change transition
      let last = this.sliderPhotos.length-1
      let item = this.sliderPhotos[last].url
      
      this.sliderPhotos.splice(0, 0, {url: item}) // change position of last Photo to index 0
      this.sliderPhotos.splice(this.sliderPhotos.length-1, 1) // remove last Photo from array
      
      setTimeout(() => {
        this.disabled = false;
      }, 700); //After transition is finished, enable button again
    },

    prev(){
      this.disabled = true;
      this.transitionName = 'prev'
      let item = this.sliderPhotos[0].url
      
      this.sliderPhotos.splice(0, 1)
      this.sliderPhotos.splice(this.sliderPhotos.length, 0, {url: item})
     
      setTimeout(() => {
        this.disabled = false;
      }, 700);
    },

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

.slider {
  display: grid;
  grid-template-columns: repeat(12,1fr);
  grid-column-gap: 20px;
  grid-row-gap: 20px;
  grid-column: 1 / 13;
  grid-row: 4 / 8;
  align-self: center;
  
  & * {
    transition: all .7s;
  }
  
  &--1{
    display: flex;
    grid-column: 1 / 9;
    grid-row: 1 / span 1;
    justify-self: end;
    overflow: hidden;
    transition: all 1s;
    position: relative;
    z-index: 10;
    width: 100vw;
    justify-content: flex-end;
  }

  &--2 {
    display: flex;
    grid-column: 1 / 7;
    grid-row: 2 / span 1;
    justify-self: end;
    overflow: hidden;
    position: relative;
    z-index: 10;
    width: 100vw;
    justify-content: flex-end;
  }

  &__photo {
    height: 160px;

    & img {
      height: 100%;
      margin: 0 5px;
      border-radius: 5px;
    }
  }

  &__text {
    grid-column: 9 / 13;
    grid-row: 1 / span 2;
    font-size: 18px;
    color: #484A4C;
    line-height: 26px;
  }

  &__controls {
    display: flex;
    align-items: end;
    justify-content: start;
    flex-direction: column;
    grid-column: 8 / span 1;
    z-index: 10;
    margin-right: 10px;

    &--prev {
      background-color: white;
      border: 1px solid rgb(31, 59, 117);
      border-radius: 5px;
      cursor: pointer;
      outline: none;
      width: 100%;
      padding: 20px 15px;
    }

    &--next {
      background-color: white;
      border: 1px solid rgb(31, 59, 117);
      border-radius: 5px;
      cursor: pointer;
      outline: none;
      width: 100%;
      padding: 20px 15px;
      margin-top: 20px;
    }
  }
}


h2 {
  margin: 0;
  color: #134880;
  font-size: 32px;
  line-height: 40px;
}

// Transition styles

.prev-enter-active {
  transition: none;
  transform: translateX(100%); 
}

.prev-leave-active {
  position: absolute;
  left: 0;
  opacity: 0;
}

.next-leave-active {
  position: absolute;
  transform: translateX(100%);
  z-index: 1;
}

.next-enter-active {
  opacity: 0;
  transition: all .2s;
  transform: translateX(-100%);
}

</style>
