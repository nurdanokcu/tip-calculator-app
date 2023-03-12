<script>
import ButtonComponent from './components/ButtonComponent.vue'
import ContainerTip from './components/ContainerTip.vue'
import DollarIcon from './components/icons/DollarIcon.vue'
import PersonIcon from './components/icons/PersonIcon.vue'
import AttributeComponent from './components/AttributeComponent.vue'

export default {
  components: { ButtonComponent, ContainerTip, DollarIcon, PersonIcon, AttributeComponent },
  data() {
    return {
      percentages: [5, 10, 15, 25, 50],
      bill: '',
      tip: 0,
      customTip: '',
      people: ''
    }
  },
  methods: {
    selectTip(percentage) {
      if (this.tip === percentage) {
        this.tip = 0
      } else {
        this.tip = percentage
        this.customTip = ''
      }
    },
    handleCustomTip(event) {
      this.customTip = event.target.value
      this.tip = 0
    },

    calculateTipAmount() {
      if (this.people) {
        return (this.bill * this.tipPercentage) / 100 / this.people
      }
    },
    reset() {
      this.tip = 0
      this.customTip = ''
      this.people = ''
      this.bill = ''
    }
  },
  computed: {
    tipAmount() {
      return this.calculateTipAmount()
    },
    tipPercentage() {
      return this.customTip ? this.customTip : this.tip
    },
    billPerPerson() {
      return this.bill / this.people + this.tipAmount
    },
    resetButtonActive() {
      return Boolean(this.tip || this.bill || this.customTip || this.people)
    }
  }
}
</script>

<template>
  <div class="main-container">
    <img class="logo" src="./assets/SPLITTER.png" alt="splitter" />
    <div class="main">
      <div class="bill">
        <div>
          <label class="bill__text" for="input-bill"> Bill </label>
          <div class="input-container">
            <i class="input-icon">
              <DollarIcon />
            </i>
            <input
              class="input input-bill"
              placeholder="0"
              v-model="bill"
              id="input-bill"
              inputmode="numeric"
              type="number"
            />
          </div>
        </div>

        <div>
          <p class="bill__text">Select Tip %</p>
          <div class="bill__buttons">
            <ButtonComponent
              @percentageClicked="selectTip"
              v-for="percentage in percentages"
              :key="percentage"
              :percentage="percentage"
              :tip="tip"
            />
            <input
              class="custom-input"
              @input="handleCustomTip"
              :value="customTip"
              type="number"
              placeholder="Custom"
            />
          </div>
        </div>

        <div>
          <div class="people-text">
            <label class="bill__text" for="input-people"> Number of People </label>
            <p v-if="people === 0" class="people-warning">Can’t be zero</p>
          </div>
          <div class="input-container">
            <i class="input-icon">
              <PersonIcon />
            </i>
            <input
              :class="['input', 'input-people', { warning: people === 0 }]"
              placeholder="0"
              v-model="people"
              id="input-people"
              inputmode="numeric"
              type="number"
            />
          </div>
        </div>
      </div>

      <ContainerTip
        :tipAmount="tipAmount"
        :billPerPerson="billPerPerson"
        @onReset="reset"
        :resetButtonActive="resetButtonActive"
      />
    </div>
  </div>
  <AttributeComponent />
</template>

<style>
.main-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 80px;
}
.logo {
  height: 52px;
}
.bill {
  max-width: 380px;
  display: flex;
  flex-direction: column;
  gap: 40px;
}
.custom-input {
  background: #f3f9fa;
  border-radius: 5px;
  border: none;
  padding: 6px 14px;
  font-family: 'Space Mono';
  font-style: normal;
  font-weight: 700;
  font-size: 22px;
  line-height: 36px;
  text-align: center;
  color: #00474b;
  border: 2px solid transparent;
  width: 100%;
  height: 48px;
  border: none;
  outline: none;
  cursor: pointer;
}
.custom-input::placeholder {
  color: #547878;
  font-family: 'Space Mono';
}
.bill__text {
  font-weight: 700;
  font-size: 16px;
  line-height: 24px;
  color: var(--color-text);
}

.input-container {
  position: relative;
  margin-top: 6px;
}
.input {
  background: #f3f9fa;
  border-radius: 5px;
  outline: none;
  border: 2px solid transparent;
  width: 100%;
  text-align: right;
  padding: 6px 18px;
  font-weight: 700;
  font-size: 24px;
  line-height: 36px;
  color: var(--color-main);
  font-family: 'Space Mono', monospace;
  cursor: pointer;
}
.input:focus,
.custom-input:focus {
  border: 2px solid #26c2ae;
}
.input-icon {
  position: absolute;
  left: 18px;
  top: 50%;
  transform: translateY(-56%);
  z-index: 2;
  height: 16px;
}
.input::placeholder {
  color: #9ebbbd;
  font-family: 'Space Mono', monospace;
}

.bill__buttons {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px 14px;
  margin-top: 6px;
}

.input-people.warning {
  border: 2px solid var(--color-input-warning);
}
.people-text {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.people-warning {
  line-height: 24px;
  color: #e17457;
}

/* mobile styles start here */
@media screen and (max-width: 992px) {
  .main {
    flex-direction: column;
  }

  .main-container {
    gap: 40px;
    padding-top: 40px;
  }
  .bill__buttons {
    grid-template-columns: repeat(2, 1fr);
    gap: 16px 14px;
  }
}
</style>
