<template>
  <div class="checkout">
    <template v-if="!showResultText">
      <h2>Payment</h2>
      <v-form @submit="handleSubmit">
        <div class="tabs">
          <div class="tab">
            <div class="tab__title" @click="activeTab = 0">
              <input type="radio" name="tabs" id="tab1" :checked="activeTab === 0" />
              <label for="tab1">Paypal</label>
            </div>
            <div class="tab__content" v-if="activeTab === 0">Pay with paypal</div>
          </div>
          <div class="tab">
            <div class="tab__title" @click="activeTab = 1">
              <input type="radio" name="tabs" id="tab2" :checked="activeTab === 1" />
              <label for="tab2">Card</label>
            </div>
            <div class="tab__content" v-if="activeTab === 1">
              <saved-cards :cards="cards" @select="selectedCard = $event" />
              <modal ref="modal" v-if="showAddModal" @close="showAddModal = false">
                <add-card-form @add="addCard" />
              </modal>
              <v-button @click="showAddModal = true">Add new card</v-button>
            </div>
          </div>
        </div>
        <v-button class="submit" type="submit">Submit order</v-button>
      </v-form>
    </template>
    <div class="checkout__result" v-show="showResultText">{{ resultText }}</div>
  </div>
</template>

<script>
import VForm from "@/ui/components/form/VForm";
import VButton from "@/ui/components/button/VButton";
import Modal from "@/ui/components/modal/Modal";
import AddCardForm from "@/components/AddCardForm";
import SavedCards from "@/components/SavedCards";

export default {
  name: "CheckoutForm",
  components: {SavedCards, AddCardForm, Modal, VButton, VForm },
  data: () => ({
    showAddModal: false,
    activeTab: 0,
    cards: [],
    selectedCard: null,
    resultText: 'Order sent! Thank you!',
    showResultText: false
  }),
  methods: {
    addCard(number) {
      if (this.cards.includes(number)) return;
      this.cards.push(number);
      this.$refs.modal.handleClose();
    },
    handleSubmit() {
      if (!this.selectedCard) return;
      this.showResultText = true;
      this.clearOrder();
      setTimeout(() => {
        this.showResultText = false;
      }, 3000);
    },
    clearOrder() {
      this.cards = [];
      this.selectedCard = null;
    }
  }
};
</script>

<style lang="scss" scoped>
  .checkout {
    max-width: 400px;
    margin: 0 auto;
    padding-top: 70px;
    text-align: left;
  }
  .tab {

    &:not(:last-child) {
      margin-bottom: 10px;
    }
    &__title {
      font-size: 16px;
      font-weight: bold;
      label {
        margin-left: 10px;
      }
    }
    &__content {
      padding: var(--indent-xs) 0 var(--indent-sm) var(--indent-md);
    }
  }
  .submit {
    margin-top: 45px;
  }
</style>
