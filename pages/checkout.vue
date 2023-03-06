<template>
  <div>
    <h1>ツイッターキャンペーン年間プラン</h1>
    <h2>19800円(税込)/年間</h2>
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
          price: process.env.price, // The id of the one-time price you created in your Stripe dashboard
          quantity: 1,
        },
      ],
      successURL: process.env.baseUrl,
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
