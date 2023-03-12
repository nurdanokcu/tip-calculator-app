<script>
export default {
  props: {
    percentage: Number,
    tip: Number
  },
  emits: ['percentageClicked']
}
</script>

<template>
  <button
    type="button"
    :class="['button', { active: tip === percentage }]"
    @click="this.$emit('percentageClicked', percentage)"
  >
    {{ percentage }}%
  </button>
</template>

<style scoped>
.button {
  background: #00474b;
  border-radius: 5px;
  border: none;
  padding: 6px 14px;
  font-family: 'Space Mono';
  font-style: normal;
  font-weight: 700;
  font-size: 24px;
  line-height: 36px;
  text-align: center;
  color: #ffffff;
  width: 100%;
  height: 48px;
  cursor: pointer;
}

.button.active {
  background-color: #9fe8df;
  color: #00474b;
}
</style>
