<template>
  <button-full
    @click.native="addToCart(product)"
    :disabled="isProductDisabled"
    data-testid="addToCart"
    class="addToCart"
  >
    <!-- changed the text of the Add to Cart button to Added -->
    <span v-if="!isAddingToCart && !isAdded">{{ $t('Add to cart') }}</span>
    <span v-if="!isAddingToCart && isAdded">{{ $t('Added') }}</span>
    <!-- Add a spinner in the Add to Cart button [Challenge 1]-->
    <Spinner v-if="isAddingToCart" />
  </button-full>
</template>

<style lang="scss" scoped>
.addToCart{
  @media (max-width: 767px) {
      height: 48px !important;
      padding: 0 !important;
  }
}
</style>

<script>
import { formatProductMessages } from '@vue-storefront/core/filters/product-messages';
import { notifications } from '@vue-storefront/core/modules/cart/helpers';
import focusClean from 'theme/components/theme/directives/focusClean';
import ButtonFull from 'theme/components/theme/ButtonFull.vue';
import Spinner from './Spinner';
import { mapGetters, mapActions } from 'vuex';
// import { log } from 'util';

export default {
  directives: { focusClean },
  components: { ButtonFull, Spinner },
  props: {
    product: {
      required: true,
      type: Object
    },
    disabled: {
      type: Boolean,
      default: false
    }
  },
  data: () => ({
    isAdded: false
  }),
  methods: {
    ...mapActions('ui', ['toggleMicrocart']),
    onAfterRemovedVariant () {
      this.$forceUpdate();
    },
    async addToCart (product) {
      try {
        const diffLog = await this.$store.dispatch('cart/addItem', {
          productToAdd: product
        });
        diffLog.clientNotifications.forEach(notificationData => {
          // Removed the Green Notification [Challenge 1]
          // this.notifyUser(notificationData);

          this.isAdded = true;
          // open the Cart [Challenge 1]
          this.toggleMicrocart();
        });
      } catch (message) {
        this.notifyUser(
          notifications.createNotification({ type: 'error', message })
        );
      }
    },
    notifyUser (notificationData) {
      this.$store.dispatch('notification/spawnNotification', notificationData, {
        root: true
      });
    }
  },
  computed: {
    ...mapGetters({
      isAddingToCart: 'cart/getIsAdding'
    }),
    isProductDisabled () {
      return (
        this.disabled ||
        formatProductMessages(this.product.errors) !== '' ||
        this.isAddingToCart
      );
    }
  },
  beforeMount () {
    this.$bus.$on('product-after-removevariant', this.onAfterRemovedVariant);
  },
  beforeDestroy () {
    this.$bus.$off('product-after-removevariant');
  }
};
</script>
