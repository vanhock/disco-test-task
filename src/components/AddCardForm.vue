<template>
  <v-form>
    <v-input label="Holder name" name="name" required />
    <v-input label="Card number" name="number" required />
    <v-input label="Expiry" name="expiry" placeholder="MM/YY" required />
    <v-input label="CVV" name="cvv" required />
    <v-button>Add card</v-button>
  </v-form>
</template>

<script>
import VForm from "@/ui/components/form/VForm";
import VInput from "@/ui/components/input/VInput";
import VButton from "@/ui/components/button/VButton";
export default {
  name: "AddCardForm",
  components: { VButton, VInput, VForm },
};
</script>

<style scoped></style>
