<template>
  <div class="cartcontrol">
    <transition name="move">
      <div class="cart-decrease icon-remove_circle_outline" @click="decreaseCart" v-show="food.count>0"></div>
    </transition>
    <div class="cart-count" v-show="food.count>0">{{food.count}}</div>
    <div class="cart-add icon-add_circle" @click="addCart"></div>
  </div>
</template>
<script>
import Vue from 'vue'
  export default{
    props:{
      food:{
        type:Object
      }
    },
    methods:{
      addCart(event){
        if(!event._constructed){
          return
        }
        if(!this.food.count){
          Vue.set(this.food,'count',1)
        }else{
          this.food.count++
        }
        this.$root.eventHub.$emit('cart.add', event.target)
      },
      decreaseCart(event){
        if(!event._constructed){
          return
        }
        if(this.food.count){
          this.food.count--
        }
      }
    }
  }
</script>
<style lang="stylus">
  .cartcontrol
    font-size:0
    .cart-decrease
      display:inline-block
      font-size:24px
      line-height:24px
      color:rgb(0,160,220)
      opacity:1
      transform:translated3D(0,0,0) rotate(0)
      &.move-enter-active,&.move-leave-active
        transition:all 0.4s linear
      &.move-enter,&.move-leave-active
        opacity:0
        transform:translate3D(24px,0,0) rotate(180deg)
    .cart-count
      display:inline-block
      vertical-align:top
      width:12px
      text-align:center
      line-height:24px
      font-size:10px
      color:rgb(147,153,159)
    .cart-add
      display:inline-block
      font-size:24px
      line-height:24px
      color:rgb(0,160,220)
</style>