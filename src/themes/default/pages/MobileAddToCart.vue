<template>
  <transition name="show-fade">
    <div class="mobile-add-to-cart hidden-md" v-show="show">
      <AddToCart
        :product="getCurrentProduct"
        :disabled="isAddToCartDisabled"
      />
    </div>
  </transition>
</template>

<script>
import AddToCart from 'theme/components/core/AddToCart.vue';

export default {
  components: {
    AddToCart
  },
  // props: ['getCurrentProduct', 'isAddToCartDisabled'],
  props: {
    getCurrentProduct: {
      type: Object,
      default: null
    },
    isAddToCartDisabled: {
      type: Boolean,
      default: false
    }
  },
  data: () => ({
    show: false
  }),
  created () {
    window.addEventListener('scroll', this.handleScroll);
  },
  destroyed () {
    window.removeEventListener('scroll', this.handleScroll);
  },
  methods: {
    handleScroll (event) {
      this.show = window.scrollY > 440 && window.scrollY < 1750
    }
  }
}
</script>

<style lang="css" scoped>
 .show-fade-enter-active,
  .show-fade-leave-active {
    transition: opacity .7s;
  }

  .show-fade-enter,
  .show-fade-leave-to {
    opacity: 0;
  }
.mobile-add-to-cart{
  z-index: 3;
  position: fixed;
  bottom: 0;
  margin: 20px;
  max-height: 48px;
  width: calc(100% - 104px);
  background: #333;
}
</style>
