<template>
  <v-form @submit="addCard">
    <v-input label="Holder name" name="name" required />
    <v-input label="Card number" name="number" type="number" required />
    <v-input label="Expiry" name="expiry" placeholder="MM/YY" type="number" required />
    <v-input label="CVV" name="cvv" type="number" required />
    <div class="invalid" v-if="!valid">Form not valid</div>
    <v-button class="add" type="submit">Add card</v-button>
  </v-form>
</template>

<script>
import VForm from "@/ui/components/form/VForm";
import VInput from "@/ui/components/input/VInput";
import VButton from "@/ui/components/button/VButton";
export default {
  name: "AddCardForm",
  components: { VButton, VInput, VForm },
  data: () => ({
    fields: {},
    valid: true
  }),
  methods: {
    addCard(fields) {
      this.fields = fields;
      const values = fields && Object.values(fields);
      const isValid = values?.every(({ valid }) => valid);
      if (!isValid) {
        this.valid = false;
        return
      }
      this.valid = true;
      const number = values.find(({name}) => name === 'number');
      const partNumber = `${number.value}`.substr(`${number.value}`.length - 4);
      this.$emit('add', partNumber);
    }
  }
};
</script>

<style lang="scss">
.flex {
  display: flex;
  align-items: flex-start;
}
.v-input {
  &:not(:last-child) {
    margin-bottom: var(--indent-md);
  }
}
.add {
  margin: 0 auto;
}
.invalid {
  text-align: center;
  margin: var(--indent-sm) 0;
}
</style>
