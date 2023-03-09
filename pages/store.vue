<template>
  <div>
    <h3>ツイッターキャンペーン年間プラン</h3>
    <p>XX,XXX円(税込)/年間</p>
    <stripe-checkout
      ref="checkoutRef"
      mode="subscription"
      :pk="publishableKey"
      :line-items="lineItems"
      :success-url="successURL"
      :cancel-url="cancelURL"
      @loading="v => loading = v"
    />
    <button @click="submit">利用を開始する</button>
  </div>
</template>

<script>
import { StripeCheckout } from '@vue-stripe/vue-stripe';
export default {
  components: {
    StripeCheckout,
  },
  data () {
    this.publishableKey = process.env.stripeApiKey;
    return {
      loading: false,
      lineItems: [
        {
          price: process.env.price,
          quantity: 1,
        },
      ],
      successURL: `${process.env.baseUrl}/success`,
      cancelURL: process.env.baseUrl,
    };
  },
  methods: {
    submit () {
      // You will be redirected to Stripe's secure checkout page
      this.$refs.checkoutRef.redirectToCheckout();
    },
  },
};
</script>
