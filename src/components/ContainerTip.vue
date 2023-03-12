<script>
export default {
  props: {
    tipAmount: Number,
    billPerPerson: Number,
    resetButtonActive: Boolean
  },
  emits: ['onReset']
}
</script>

<template>
  <div class="tip">
    <div class="tip__section tip__section-first">
      <div class="tip__text">
        <p class="tip__text-big">Tip Amount</p>
        <p class="tip__text-small">/ person</p>
      </div>
      <p class="tip__number">${{ tipAmount ? tipAmount.toFixed(2) : '0.00' }}</p>
    </div>

    <div class="tip__section tip__section-second">
      <div class="tip__text">
        <p class="tip__text-big">Total</p>
        <p class="tip__text-small">/ person</p>
      </div>
      <p class="tip__number">${{ tipAmount ? billPerPerson.toFixed(2) : '0.00' }}</p>
    </div>

    <button
      @click="this.$emit('onReset')"
      :class="['tip__reset', { 'active-button': resetButtonActive }]"
      :disabled="!resetButtonActive"
      type="button"
    >
      RESET
    </button>
  </div>
</template>

<style scoped>
.tip {
  padding: 40px;
  background-color: var(--color-main);
  border-radius: 15px;
  max-width: 420px;
}
.tip__section {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.tip__section-first {
  margin-bottom: 25px;
}
.tip__section-second {
  margin-bottom: 120px;
}
.tip__text-big {
  line-height: 24px;
  color: #fff;
  min-width: 172px;
}
.tip__text-small {
  font-size: 13px;
  line-height: 19px;
  color: #7f9d9f;
}

.tip__number {
  font-weight: 700;
  font-size: 48px;
  line-height: 71px;
  letter-spacing: -1px;
  color: #26c2ae;
}

.tip__reset {
  display: block;
  padding: 9px 132px;
  margin: 0 auto;
  background: #0d686d;
  border-radius: 5px;
  font-family: 'Space Mono';
  font-style: normal;
  font-weight: 700;
  font-size: 20px;
  line-height: 30px;
  text-align: center;
  cursor: pointer;
  color: #00474b;
  opacity: 0.35;
  border: none;
}
.tip__reset:active {
  background: #9fe8df;
}

.active-button.tip__reset {
  background: #26c2ae;
  opacity: 1;
}
@media screen and (max-width: 992px) {
  .tip {
    max-width: 350px;
  }

  .tip__section-first {
    margin-bottom: 15px;
  }

  .tip__section-second {
    margin-bottom: 32px;
  }

  .tip__reset {
    padding: 9px 100px;
  }
  .tip__number {
    font-size: 36px;
  }

  .tip__text-big {
    min-width: fit-content;
  }
}
</style>
