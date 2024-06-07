<template>
  <div class="calculator-wrapper">
    <h1 class="calculator-header">
      <span>Koosta soovinimekiri</span> ja vaata oma uue sisustuse kuumakset
    </h1>
    <div class="calculator">
      <div class="product-table">
        <div class="table-left">
          <p class="table-title">TOODE</p>
          <p
            class="table-row"
            v-for="(name, index) in productNames"
            :key="index"
          >
            {{ name }}
          </p>
          <BaseButton class="product-add" :format="FORMATS.TERTIARY">
            <template #left-icon>
              <img src="@/assets/icons/circle-plus.svg" alt="circle-plus" />
            </template>
            Lisa toode
          </BaseButton>
        </div>
        <div class="table-right">
          <p class="table-title">HIND</p>
          <p
            class="table-row table-row-price"
            v-for="(price, index) in productPrices"
            :key="index"
          >
            {{ price }} <span class="product-price-symbol">€</span>
          </p>
          <BaseButton class="product-delete" :format="FORMATS.TERTIARY">
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
          <BaseButton class="request-button">Taotle sisustuslaenu</BaseButton>
          <p class="condition-button">Tutvu tingimustega</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import BaseButton from "@/components/base_components/BaseButton.vue";
import { FORMATS } from "@/enums/components";
import { ref, computed } from "vue";

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
const productAmount = productPrices.value.reduce((a, b) => a + b, 0);
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
}

.calculator-header {
  text-align: center;
  letter-spacing: -0.005rem;
  width: 38.38rem;
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
  width: 38.56rem;
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
  color: #6c6972;
}

.product-delete {
  color: #6c6972;
  align-self: end;
}

.table-left {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  width: 13.25rem;
}

.table-right {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  width: 8.25rem;
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
}

.request-button {
  padding: 0.88rem 1rem;
  border-radius: 0.25rem;
  width: 100%;
  font-size: 0.88rem;
  line-height: 1.25rem;
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
}

.condition-button {
  font-size: 0.88rem;
  line-height: 1.25rem;
  font-weight: 400;
  color: #6c6972;
  border-bottom: 0.06rem solid #6c6972;
  width: fit-content;
}
</style>
