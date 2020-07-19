<template>
  <button
    type="button"
    class="menu"
    @click="openMenu"
    :aria-label="$t('Open menu')"
    data-testid="menuButton"
  >
    <div :class="opening ? 'active-menu' :'menu-line'" />
    <div :class="opening ? 'active-menu' :'menu-line'" />
    <div :class="opening ? 'active-menu' :'menu-line'" />
  </button>
</template>

<style lang="css" scoped>
  .menu{
    width: 50px;
    height: 50px;
    background: transparent;
    border: none;
  }
  .menu-line {
    width: 100%;
    height: 2px;
    background: black;
    margin: 5px 0px;
    transition: 0.2s;
  }
  .active-menu {
    width: 100%;
    height: 2px;
    background: black;
    margin: 5px 0px;
    transition: 0.2s;
  }

  .active-menu:nth-child(1) {
    transform: rotate(45deg);
  }
  .active-menu:nth-child(2) {
    display: none;
  }
  .active-menu:nth-child(3) {
    margin-top: -8px;
    transform: rotate(-45deg);
  }
</style>

<script>
import HamburgerIcon from '@vue-storefront/core/compatibility/components/blocks/Header/HamburgerIcon'
import { mapState } from 'vuex'

export default {
  mixins: [HamburgerIcon],
  data: () => ({
    opening: false

  }),
  computed: mapState({
    isOpen: state => state.ui.sidebar
  }),
  methods: {
    openMenu () {
      this.opening = !this.opening
      setTimeout(() => {
        this.openSidebarMenu()
      }, 200);
    }
  },

  watch: {
    isOpen (newVal, oldVal) {
      if (newVal === false) {
        this.opening = false
      }
    }
  }
}
</script>
