<template>
  <div class="calculator">
    <div class="container">
      <input class="displayBox" type="text" v-model="result" />
      <br />
      <div :key="buttonArr" v-for="buttonArr in buttons" class="btns">
        <div :key="button" v-for="button in buttonArr">
          <Button
            :text="button"
            @onClick="onButtonClick(button)"
            :disableButtons="disableButtons"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Button from "./Button.vue";

export default {
  name: "Calculator",
  data() {
    return {
      buttons: [
        ["1", "2", "3", "+"],
        ["4", "5", "6", "-"],
        ["7", "8", "9", "*"],
        ["0", "C", "/", "="],
      ],
      previous: "",
      next: "",
      result: "0",
      operator: "",
      disableButtons: false,
    };
  },
  components: {
    Button,
  },
  // updated() {
  //   if (this.operator)
  //   this.result = "Loading";
  //   setTimeout(() => {
  //     this.result = "";
  //     console.log(this.result);
  //   }, 1000);
  // },
  watch: {
    next: function () {
      const temp = this.result;
      console.log(temp);
      this.result = "Loading";
      this.disableButtons = true;
      setTimeout(() => {
        this.result = temp;
        this.disableButtons = false;
      }, 2000);
    },
  },
  methods: {
    onButtonClick(text) {
      if (new RegExp("[0-9]+").test(text)) {
        if (this.result === "0") this.result = "";
        this.next = this.next + text;
        this.result = this.next;
      } else if (new RegExp("[+|\\-|*|/|%]").test(text)) {
        this.result = "";
        this.previous = this.next;
        this.next = "";
        this.operator = text;
      } else if (new RegExp("C").test(text)) {
        this.previous = "";
        this.next = "";
        this.result = "0";
        this.operator = "";
      } else if (new RegExp("=").test(text)) {
        if (this.operator && this.previous && this.next) {
          const prev = parseInt(this.previous);
          const next = parseInt(this.next);

          switch (this.operator) {
            case "+": {
              this.result = prev + next + "";
              break;
            }
            case "-": {
              this.result = prev - next + "";
              break;
            }
            case "*": {
              this.result = prev * next + "";
              break;
            }
            case "/": {
              this.result = prev * next + "";
              break;
            }
          }

          this.previous = "";
          this.next = this.result;
        }
      }
    },
  },
};
</script>

<style scoped>
.calculator {
  margin: auto;
  height: 320px;
  width: 600px;
  border: 1px solid black;
}

.container {
  margin-left: 20px;
}

.displayBox {
  margin-top: 5px;
  width: 556px;
  height: 50px;
  font-size: 24px;
}

.btns {
  display: flex;
}
</style>
