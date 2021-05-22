<template>
  <div class="checkout">
    <h2>Payment</h2>
    <v-form>
      <div class="tabs">
        <div class="tab">
          <div class="tab__title">
            <input type="radio" name="tabs" id="tab1" />
            <label for="tab1">Paypal</label>
          </div>
          <div class="tab__content">Pay with paypal</div>
        </div>
        <div class="tab">
          <div class="tab__title">
            <input type="radio" name="tabs" id="tab2" />
            <label for="tab2">Paypal</label>
          </div>
          <div class="tab__content">
            <h3>Pay with card</h3>
            <saved-cards />
            <modal v-if="showAddModal">
              <add-card-form />
            </modal>
            <v-button>Add new card</v-button>
          </div>
        </div>
      </div>
      <v-button-wide>Submit order</v-button-wide>
    </v-form>
  </div>
</template>

<script>
import VForm from "@/ui/components/form/VForm";
import VButtonWide from "@/ui/components/button/VButtonWide";
import VButton from "@/ui/components/button/VButton";
import SavedCards from "@/components/SavedCards";
import Modal from "@/ui/components/modal/Modal";
import AddCardForm from "@/components/AddCardForm";

export default {
  name: "CheckoutForm",
  components: { AddCardForm, Modal, SavedCards, VButton, VButtonWide, VForm },
  data: () => ({
    showAddModal: false,
  }),
};
</script>

<style scoped></style>
