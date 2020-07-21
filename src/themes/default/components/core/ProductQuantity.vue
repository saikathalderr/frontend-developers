<template>
  <div class="product-quantity">
    <!-- <base-input-number
      :name="name"
      :value="value"
      :min="1"
      :max="max"
      :disabled="disabled"
      @input="$emit('input', $event)"
      @blur="$v.$touch()"
      only-positive
      :validations="[
        {
          condition: !$v.value.numeric || !$v.value.minValue || !$v.value.required,
          text: $t(`Quantity must be positive integer`)
        },
        {
          condition: maxQuantity && value && !$v.value.maxValue,
          text: $t('Quantity must be below {quantity}', { quantity: maxQuantity })
        }
      ]"
    /> -->
    <select name="productQuantity" id="productQuantity" v-model="quantity" v-if="!loading && max > 0" @change="onQuantityChange()" style="height: unset">
      <option v-for="(stock, index) in max" :key="index" :value="stock">
        {{ stock }}
      </option>
    </select>
    &nbsp;&nbsp;&nbsp;&nbsp;
    <span v-if="!loading && max > 0">
      {{ max }} In Stock
    </span>
    <spinner v-if="loading" />
    <h3 v-if="!loading && max === 0">
      Out of stock
    </h3>
  </div>
</template>

<script>
import { minValue, maxValue, numeric, required } from 'vuelidate/lib/validators'
import { onlineHelper } from '@vue-storefront/core/helpers'
// import BaseInputNumber from 'theme/components/core/blocks/Form/BaseInputNumber'
import Spinner from 'theme/components/core/Spinner'

export default {
  components: {
    Spinner
    // BaseInputNumber
  },
  props: {
    value: {
      type: [Number, String],
      required: true
    },
    showQuantity: {
      type: Boolean,
      default: false
    },
    maxQuantity: {
      type: Number,
      default: undefined
    },
    checkMaxQuantity: {
      type: Boolean,
      default: true
    },
    loading: {
      type: Boolean,
      default: false
    },
    isSimpleOrConfigurable: {
      type: Boolean,
      default: false
    }
  },
  data: function () {
    return {
      quantity: this.value
    };
  },
  computed: {
    isOnline (value) {
      return onlineHelper.isOnline
    },
    max () {
      if (!this.isOnline || !this.isSimpleOrConfigurable) {
        return null
      }

      return this.maxQuantity
    },
    disabled () {
      if (!this.isOnline) {
        return false
      }
      return !this.maxQuantity && this.checkMaxQuantity && this.isSimpleOrConfigurable
    },
    name () {
      if (this.isSimpleOrConfigurable && !this.loading && this.showQuantity) {
        return this.$i18n.t(this.isOnline ? 'Quantity available' : 'Quantity available offline', { qty: this.maxQuantity })
      }
      return this.$i18n.t('Quantity')
    }
  },
  validations () {
    return {
      value: {
        minValue: minValue(1),
        maxValue: maxValue(this.max) && !this.isSimpleOrConfigurable,
        numeric,
        required
      }
    }
  },
  watch: {
    '$v.$invalid' (error) {
      this.$emit('error', error)
    }
  },
  methods: {
    onQuantityChange () {
      // console.log('yo', this.quantity);
      this.$emit('input', this.quantity)
      this.$v.$touch()
    }
  }
}
</script>
<style lang="scss" scoped>
.product-quantity {
  position: relative;
  /deep/ .spinner {
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    margin: auto;
  }
}
</style>
