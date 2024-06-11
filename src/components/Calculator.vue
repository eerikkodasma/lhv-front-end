<template>
  <div class="calculator-wrapper">
    <h1 class="calculator-header">
      <span>Koosta soovinimekiri</span> ja vaata oma uue sisustuse kuumakset
    </h1>
    <div id="calculator" class="calculator">
      <div class="product-table">
        <div class="table-left">
          <p class="table-title">TOODE</p>
          <BaseInput
            v-for="(_, index) in productNames"
            :key="index"
            :model-value="products[index].name"
            class="table-input"
            :id="`product-${index}`"
            name="product"
            type=""
            placeholder="Type here..."
            @update:model-value="
              (value) => (products[index] = { ...products[index], name: value })
            "
          />
          <BaseButton
            class="product-add"
            :format="FORMATS.TERTIARY"
            @click="addProduct"
          >
            <template #left-icon>
              <img src="@/assets/icons/circle-plus.svg" alt="circle-plus" />
            </template>
            Lisa toode
          </BaseButton>
        </div>
        <div class="table-right">
          <p class="table-title">HIND</p>
          <BaseInput
            class="table-input"
            v-for="(_, index) in productPrices"
            :key="index"
            :model-value="products[index].price"
            :id="`amount-${index}`"
            name="amount"
            type="number"
            placeholder="Type here..."
            acceptsCommas
            @update:model-value="
              (value) =>
                (products[index] = { ...products[index], price: value })
            "
          >
            <template #iconAfter
              ><span class="product-price-symbol">€</span></template
            >
          </BaseInput>
          <BaseButton
            class="product-delete"
            :format="FORMATS.TERTIARY"
            @click="removeLastProduct"
          >
            <template #left-icon>
              <img src="@/assets/icons/trash.svg" alt="trash" />
            </template>
            Kustuta
          </BaseButton>
        </div>
      </div>
      <div class="product-right">
        <p class="table-amount">{{ productAmount }} €</p>
        <div class="action-section">
          <BaseButton class="request-button" @click="isLoanModalOpen = true"
            >Taotle sisustuslaenu</BaseButton
          >
          <p class="condition-button" @click="isConditionsModalOpen = true">
            Tutvu tingimustega
          </p>
        </div>
      </div>
    </div>
    <LoanPersonalDetailsModal
      v-if="isLoanModalOpen"
      @close="isLoanModalOpen = !isLoanModalOpen"
    />
    <TermsAndConditions
      v-if="isConditionsModalOpen"
      @close="isConditionsModalOpen = !isConditionsModalOpen"
    />
  </div>
</template>

<script setup>
import LoanPersonalDetailsModal from "@/components/LoanPersonalDetailsModal.vue";
import TermsAndConditions from "@/components/TermsAndConditions.vue";
import BaseButton from "@/components/base_components/BaseButton.vue";
import BaseInput from "@/components/base_components/BaseInput.vue";
import { FORMATS } from "@/enums/components";
import { ref, computed } from "vue";

const isLoanModalOpen = ref(false);
const isConditionsModalOpen = ref(false);
const products = ref([
  { name: "Diivan", price: 500 },
  { name: "Lamp", price: 85 },
]);

const productNames = computed(() =>
  products.value.map((product) => product.name)
);
const productPrices = computed(() =>
  products.value.map((product) => product.price)
);

// Need to round to 2 decimal places because system calculation failures
const productAmount = computed(() =>
  productPrices.value.reduce(
    (a, b) => parseFloat((parseFloat(a || 0) + parseFloat(b || 0)).toFixed(2)),
    0
  )
);

const addProduct = () => {
  products.value = [...products.value, { name: "", price: "" }];
};

const removeLastProduct = () => {
  if (products.value.length !== 1) {
    products.value.splice(-1);
  } else {
    products.value = [{ name: "", price: "" }];
  }
};
</script>

<style scoped>
.calculator-wrapper {
  display: flex;
  flex-direction: column;
  background-color: #f1edeb;
  align-items: center;
  padding: 3.75rem;
  border-radius: 0.25rem;
  gap: 2.5rem;

  @media screen and (max-width: 600px) {
    gap: 2.5rem;
    padding: 2.5rem 1.5rem;
    border-radius: 0.25rem;
  }
}

.calculator-header {
  text-align: center;
  letter-spacing: -0.005rem;
  max-width: 38.38rem;
}

.calculator-header span {
  font-size: 1.75rem;
  line-height: 2.13rem;
  font-weight: 700;
}

.calculator {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 5rem;

  @media screen and (max-width: 600px) {
    flex-direction: column;
    gap: 2.5rem;
  }
}

.product-table {
  display: flex;
  gap: 1.88rem;
  justify-content: right;
  width: fit-content;
}

.product-right {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  gap: 1.5rem;
  width: 10rem;
}

.product-add {
  padding: 0;
  color: #6c6972;
}

.product-delete {
  padding: 0;
  color: #6c6972;
  align-self: end;
}

.table-left {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  width: 13.25rem;

  @media screen and (max-width: 600px) {
    flex: 1;
    width: auto;
  }
}

.table-right {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  width: 8.25rem;

  @media screen and (max-width: 600px) {
    flex: 1;
    width: auto;
  }
}

.table-title {
  font-size: 0.75rem;
  font-weight: 500;
  line-height: 1.13rem;
  color: #6c6972;
  text-align: left;
}

.table-row {
  border-bottom: 0.06rem solid #c6c4c7;
}

.table-row-price {
  display: flex;
  gap: 0.25rem;
  justify-content: space-between;
}

.table-amount {
  font-size: 2.81rem;
  font-weight: 200;
  line-height: 3rem;
  letter-spacing: -0.015rem;
  word-wrap: break-word;
  text-align: center;
  width: 100%;
}

::v-deep(.table-input .input) {
  background: transparent;
  border: none;
  border-bottom: 0.06rem solid #c6c4c7;
}
::v-deep(.table-input .input:focus-visible) {
  outline: 0;
}

.request-button {
  padding: 0.88rem 1rem;
  font-weight: 500;
}

.action-section {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
  width: 100%;
}

.product-price-symbol {
  color: #89868d;
  border-bottom: 0.06rem solid #c6c4c7;
}

.condition-button {
  cursor: pointer;
  padding: 0;
  color: #6c6972;
  border-bottom: 0.06rem solid #6c6972;
}
</style>
