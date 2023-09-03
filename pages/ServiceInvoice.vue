<template>
  <div class="content-widget">
    <div class="container">
      <div class="row">
        <div class="col-12 archive-header text-center pt-3 pb-3">
          <div
            class="mt-5 col-lg-6 col-md-4 col-sm-3"
            style="display: inline-block"
          >
            <div id="paypal-button-container" v-if="false" />
            <form id="payment-form">
              <div id="card-element">
                <!-- Stripe.js injects the card element here. -->
              </div>
              <p id="card-error" role="alert" class="text-danger" />
              <button id="submit-button">
                <div class="spinner hidden" id="spinner" />
                <span id="button-text">Pay now</span>
              </button>
              <p class="result-message hidden text-success">
                Payment succeeded, see the result in your
                <a href="" target="_blank">Stripe dashboard. </a>
                Refresh the page to pay again.
              </p>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { loadStripe } from "@stripe/stripe-js";
// import { loadStripe } from "@stripe/stripe-js/pure";
// loadStripe.setLoadParameters({ advancedFraudSignals: false });
// The loadStripe.setLoadParameters function is only available when
// imorting loadStripe from @stripe/stripe-js/pure.

export default {
  head() {
    return {
      script: [
        {
          src: "https://js.stripe.com/v3/",
        },
      ],
      link: [
        {
          rel: "stylesheet",
          href: "../assets/stripe.css",
        },
      ],
    };
  },
  data() {
    return {
      cardStyle: {
        base: {
          color: "#32325d",
          fontFamily: '"Arial, sans-serif',
          fontSmoothing: "antialiased",
          fontSize: "16px",
          "::placeholder": {
            color: "#32325d",
          },
        },
        invalid: {
          fontFamily: "Arial, sans-serif",
          color: "#fa755a",
          iconColor: "#fa755a",
        },
      },
    };
  },
  created() {
    this.loadStripeWhenModalOpens();
  },
  methods: {
    async loadStripeWhenModalOpens() {
      if (!stripe) {
        stripe = await loadStripe(process.env.stripePublishableKey);
        elements = stripe.elements();
      }

      const purchase = { items: [{ id: "this-is-id" }] };
      const that = this;

      this.$axios
        .post("/create-payment-intent", purchase, {
          headers: {
            "Content-Type": "application/json",
          },
        })
        .then((createPaymentIntentResponse) => {
          const elements = stripe.elements();
          const card = elements.create("card", { style: that.cardStyle });
          // Stripe injects an iframe into the DOM
          card.mount("#card-element");
          card.on("change", function (event) {
            /*
             * Disable the Pay button if there are no card details
             * in the Element.
             */
            document.querySelector("button").disabled = event.empty;
            document.querySelector("#card-error").textContent = event.error
              ? event.error.message
              : "";
          });

          const form = document.getElementById("payment-form");
          form.addEventListener("submit", function (event) {
            event.preventDefault();
            // Complete payment when the submit button is clicked
            AV.Cloud.run("createStripePaymentIntent", {
              amount: 3000, // Price in cent.
              currency: "usd",
            }).then((createStripePaymentIntentResult) => {
              that.payWithCard(
                stripe,
                card,
                createStripePaymentIntentResult?.clientSecret
              );
            });
          });
        })
        .catch((createPaymentIntentError) => {
          console.log(
            "createPaymentIntentError:",
            createPaymentIntentError.message
          );
        });
    },
    payWithCard: function (stripe, card, clientSecret) {
      this.loading(true);

      const that = this;

      stripe
        .confirmCardPayment(clientSecret, {
          payment_method: {
            card: card,
          },
        })
        .then(function (confirmCardPaymentResult) {
          if (confirmCardPaymentResult.error)
            that.showError(confirmCardPaymentResult.error.message);
          else that.completeOrder(confirmCardPaymentResult.paymentIntent.id);
        });
    },
    loading(isLoading) {
      if (isLoading) {
        document.querySelector("button").disabled = true;
        document.querySelector("#spinner").classList.remove("hidden");
        document.querySelector("#button-text").classList.add("hidden");
      } else {
        document.querySelector("button").disabled = false;
        document.querySelector("#spinner").classList.add("hidden");
        document.querySelector("#button-text").classList.remove("hidden");
      }
    },
    showError(errorMessageText) {
      this.loading(false);

      const errorMessage = document.querySelector("#card-error");
      errorMessage.textContent = errorMessageText;

      setTimeout(function () {
        errorMessage.textContent = "";
      }, 4000);
    },
    completeOrder(paymentIntentId) {
      this.loading(false);

      document
        .querySelector(".result-message a")
        .setAttribute(
          "href",
          `https://dashboard.stripe.com/test/payments/${paymentIntentId}`
        );
      document.querySelector(".result-message").classList.remove("hidden");
      document.querySelector("button").disabled = true;
    },
    destroyStripeIbanElement() {
      const ibanElement = elements?.getElement("iban");

      if (ibanElement) ibanElement.destroy();
    },
  },
  beforeDestroy() {
    this.destroyStripeIbanElement();
  },
};
</script>

<style lang="scss" scoped>

</style>
