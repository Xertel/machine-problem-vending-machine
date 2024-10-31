<script>
export default {
  data() {
    return {
      changeOutput: ""
    }
  },
  props: {
    vmData: {
      type: Object,
      required: true
    }
  },
  emits: ['update:vmData'],
  computed: {
    vmDataValue: {
      get() {
        return this.vmData
      },
      set(value) {
        this.$emit('update:vmData', value)
      }
    }
  },
  methods: {
    getChange(bill, owed) {
      const changeValues = [0, 0, 0, 0, 0, 0, 0, 0, 0];
      var change = bill - owed;
      let amount = 0;

      if (owed < 0 || owed > 1000 || bill > 1000 || change <= 0) {
        if (change < 0) this.changeOutput = "Please put more money.";
        if (change == 0) this.changeOutput = "There is no more change." + "<br><br>" + "Thanks for shopping!";
        if (owed > 1000) this.changeOutput = "You owe too much!";
        if (bill > 1000 || owed < 0) this.changeOutput = "Invalid input!";

        return null;
      } else {
        for (let i = 0; i <= 8; i++) {
          amount = this.vmDataValue.denominations[i];
          while (change >= amount && change > 0) {
            change -= amount;
            changeValues[i]++;
          }
        }
        this.changeOutput = "Here's your change:"
        return changeValues;
      }
    },
    clearValues () {
      this.vmDataValue.totalOwed = 0
      this.vmDataValue.totalMoney = 1000
    },
    changeOutputMessage(changeValues) {
      if (changeValues != null) {
        for (let i = 0; i <= 8; i++) {
          if (changeValues[i] > 0) {
            this.changeOutput += "<span style='font-size: 0.75em; line-height: 0.2em; font-weight: bold;'><br>" + changeValues[i] + "x P" + this.vmDataValue.denominations[i]
            this.changeOutput += (i < 6) ? " bill" : " coin"
            this.changeOutput += "</span>"
          }
        }
        this.changeOutput += "<br><br>" + "Thanks for shopping!"
      }
    }
  },
}
</script>

<template>
  <div class="payment-container">
    <div class="payment-header-container">
      <div>Payment</div>
      <button class="input-clear" @click="clearValues">
        <img src="https://www.freeiconspng.com/uploads/arrow-refresh-reload-icon-29.png"
        style="width:20px; height:20px;">
      </button>
    </div>
    <div class="input-container" style="margin-top: 1em;">
      <div class="input-header-container">
        <div class="input-label">Total Owed: </div>
      </div>
      <input class="input-value" type="number" v-model="vmDataValue.totalOwed" />
    </div>
    <div class="input-container">
      <div class="input-header-container">
        <div id="input-bill" class="input-label">Insert Bill: </div>
      </div>
      <select class="input-value" v-model="vmDataValue.totalMoney">
        <option value="1000">P1000</option>
        <option value="500">P500</option>
        <option value="200">P200</option>
        <option value="100">P100</option>
        <option value="50">P50</option>
        <option value="20">P20</option>
      </select>
    </div>
    <div class="button-container">
      <button class="change-button" @click="changeOutputMessage(getChange(vmData.totalMoney, vmData.totalOwed))">Get Change</button>
    </div>
    <div class="change-output" v-html="changeOutput">
    </div>
  </div>
</template>

<style scoped>
.payment-container {
  height: 100%;
  width: 40%;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  background-color: rgb(20, 20, 20);
  overflow: auto;
  padding: 1.6em;
  gap: 3em;
  border-radius: 40px;
  color: var(--lighter-text);
}

.payment-header-container {
  font-size: 2.4em;
  position: relative;
  color: var(--light-text);
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.payment-header-container > div {
  font-weight: bold;
}

.payment-header-container::after {
  content: '';
  position: absolute;
  left: 0;
  bottom: -.4em;
  height: 2px;
  width: 100%;
  background-color: var(--lighter-text);
}

.input-clear {
padding: 2px 4px;
border-radius: 6px;
}

.input-container {
  display: flex;
  flex-direction: column;
  width: 100%;
  gap: .2em;
}

.input-header-container {
  width: 100%;
  height: auto;
  display: flex;
  justify-content: space-between;
}

.input-label {
  color: black;
  font-size: 2em;
  font-weight: bold;
  color: var(--light-text);
}

.input-value {
  width: 100%;
  height: 1.6em;
  font-size: 1.8em;
  background-color: var(--light-text);
  padding-left: 10px;
}

.button-container {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 1em;
}

.change-button {
  font-size: 1.8em;
  padding: 12px;
  color: var(--lighter-text);
  background-color: rgb(41, 153, 41);
  border-color: rgb(44, 138, 44);
  border-width: 1px;
  border-radius: 16px;
  box-shadow: 2px 2px rgb(65, 65, 65);
}

.change-output {
  font-size: 1.5em;
  margin-left: 1em;
}


@media only screen and (max-width: 768px) {
  .payment-container {
    height: auto;
    width: 100%;
    flex-direction: column;
    overflow: auto;
    padding: 2em;
  }
}

</style>
