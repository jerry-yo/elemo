<template>
  <div class="carcontrol">
    <transition name="slide-fade">
      <div class="car-decrease" v-show="food.count>0"
      @click.stop.prevent="decreaseCar">
          <span class="inner  icon-remove_circle_outline"></span>
      </div>
    </transition>
    <div class="car-count" v-show="food.count>0">
      {{food.count}}
    </div>
    <div class="car-add icon-add_circle" @click.stop.prevent="addCar">

    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  import Vue from 'vue';
  export default {
    props: {
      food: {
        type: Object
      }
    },
    methods: {
      addCar (event) {
        if (!event._constructed) {
          return;
        }
        if (!this.food.count) {
          Vue.set(this.food, 'count', 1);
        } else {
          this.food.count++;
        }
        this.$emit('add', event.target);
      },
      decreaseCar (event) {
        if (!event._constructed) {
          return;
        }
        if (this.food.count) {
          this.food.count--;
        }
      }
    }
  };
</script>
<style lang="stylus" rel="stylesheet/stylus">
  .carcontrol
    font-size: 0
    .car-decrease
      display: inline-block
      opacity: 1
      transform: translate3D(0, 0, 0)
      .inner
        display: inline-block
        padding: 6px
        line-height: 24px
        font-size: 24px
        color: rgb(0, 160, 220)
        transform: rotate(-180deg)
      &.slide-fade-enter-active, &.slide-fade-leave-active
        transition: all 0.4s linear
        .inner
          transition: all 0.4s linear
      &.slide-fade-enter, &.slide-fade-leave-to
        opacity: 0
        transform: translate3D(24px, 0, 0)
        .inner
          transform: rotate(0)
    .car-count
      display: inline-block
      vertical-align: top
      width: 12px
      padding-top: 6px
      line-height: 24px
      text-align: center
      font-size: 10px
      color: rgb(147, 153, 159)
    .car-add
      display: inline-block
      padding: 6px
      line-height: 24px
      font-size: 24px
      color: rgb(0, 160, 220)


</style>
