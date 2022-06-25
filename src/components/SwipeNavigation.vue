<script setup lang="ts">
const props = defineProps({
    mySwiperClass: String,
})
interface E extends Element {
  swiper: any;
}
const swipe = (swipeTo: string) => {
  const s = (document.querySelector(`.${props.mySwiperClass}`)! as E).swiper;
  if (swipeTo === "right") s.slideNext();
  else s.slidePrev();
};
</script>

<template>
     <div class="navigation w-1/2">
      <div class="nav activate-cursor">
        <i
          class="uil uil-arrow-left activate-cursor"
          @click="swipe('left')"
        ></i>
      </div>
      <div class="nav activate-cursor">
        <i
          class="uil uil-arrow-right activate-cursor"
          @click="swipe('right')"
        ></i>
      </div>
    </div>
</template>

<style lang="scss" scoped>
.navigation {
    @include flex(row, center, space-between);
    .nav {
      @include flex(row, center, center);
      width: clamp($big-heading, 2vw, 5rem);
      height: clamp($big-heading, 2vw, 5rem);
      border: 0.15rem solid white;
      border-radius: 50%;
      color: rgb(238, 222, 222);
      transition: all 0.3s;
      i {
        font-size: clamp($medium-sub-heading, 2vw, $big-heading);
      }
      &:hover {
        transform: scale(2);
        color: cyan;
        transition: all 0.3s;
      }
    }
  }
</style>