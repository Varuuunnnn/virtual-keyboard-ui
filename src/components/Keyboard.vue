<template>
  <div>
    <!-- For input text  -->
    <textarea
      v-model="inputText"
      class="q-my-sm"
      placeholder="Please type something..."
      ref="inputText"
    ></textarea>

    <!-- Keyboard -->
    <div class="keyboard bg-grey-4 q-ma-lg q-pa-sm rounded-borde rs">
      <!-- For all the alphabetical keys -->
      <div class="alphabet-keys">
        <Key
          v-for="(key, i) in alphabetKeys"
          :key="i"
          :name="key"
          :type="'alphabetic'"
          @clicked="onClickButton"
        />
      </div>

      <!-- For all the numerical keys -->
      <div class="numeric-keys q-mt-xs">
        <Key
          v-for="(key, i) in numericKeys"
          :key="i"
          :name="key"
          :type="'numeric'"
          @clicked="onClickButton"
        />
      </div>

      <!-- For all the functional keys -->
      <div class="function-keys q-mt-xs">
        <Key
          v-for="(key, i) in functionKeys"
          :key="i"
          :name="key"
          :type="'function'"
          @clicked="onClickButton"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Key from "./Key.vue";
//keys data
import { alphabetKeys, functionKeys, numericKeys } from "../utils";

export default {
  name: "Keyboard",
  components: {
    Key
  },
  data() {
    return {
      alphabetKeys,
      functionKeys,
      numericKeys,
      inputText: "",
      capsLockStatus: false
    };
  },

  methods: {
    onClickButton(event) {
      // capturing keytype, keyname, to perform operations
      let keyType = event[0];
      let keyName = event[1];
      this.handleKeyAction(keyType, keyName);
    },

    handleKeyAction(keyType, keyName) {
      // Handling behaviour of numeric & alphabetic keys
      if (keyType === "alphabetic") {
        this.updateInputText(keyName, keyType);
        for (let i = this.alphabetKeys.length - 1; i > 0; i--) {
          const j = Math.floor(Math.random() * (i + 1));
          [this.alphabetKeys[i], this.alphabetKeys[j]] = [
            this.alphabetKeys[j],
            this.alphabetKeys[i]
          ];
        }
      } else if (keyType === "numeric") {
        this.updateInputText(keyName, keyType);
        for (let i = this.numericKeys.length - 1; i > 0; i--) {
          const j = Math.floor(Math.random() * (i + 1));
          [this.numericKeys[i], this.numericKeys[j]] = [
            this.numericKeys[j],
            this.numericKeys[i]
          ];
        }
      } else {
        // Handling behaviour of function keys
        this.handleFunctionKeyAction(keyName);
      }
      this.$refs.inputText.focus();
    },

    //update input text as per key
    updateInputText(data) {
      this.inputText += data;
    },

    //handle function keys
    handleFunctionKeyAction(keyName) {
      switch (keyName) {
        case "space": {
          // handling space
          this.inputText += " ";
          break;
        }
        case "delete": {
          // handling delete
          this.inputText = this.inputText.substring(
            0,
            this.inputText.length - 1
          );
          break;
        }
        case "enter": {
          // handling enter key
          this.inputText += "\n";
          break;
        }
        case "caps": {
          // handling capitalization
          this.capsLockStatus = !this.capsLockStatus;
          if (this.capsLockStatus) {
            this.alphabetKeys = this.alphabetKeys.map(function (alphabet) {
              return alphabet.toUpperCase();
            });
          } else {
            this.alphabetKeys = this.alphabetKeys.map(function (alphabet) {
              return alphabet.toLowerCase();
            });
          }
        }
      }
    }
  }
};
</script>

<style scoped>
.keyboard {
  max-width: 500px;
  margin: 0 auto;
}
textarea {
  border-width: 1px;
  border-style: solid;
  outline: none;
}
</style>
