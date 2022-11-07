<template>
  <div id="app">
    <div class="container">
      <!-- row one -->
      <div class="flex">
        <input type="button" class="bg-one box-one" @click="clear()" value="C" />
        <!-- <input type="text" class="bg-two box-two display" value="{{ display || '0' }}" placeholder="Result ..."
          readonly /> -->
        <div class="bg-two box-two display">{{ display || '0' }} </div>
      </div>

      <!-- row two -->
      <div class="flex">
        <input type="button" class="bg-two box-one" @click="append('7')" value="7" />
        <input type="button" class="bg-two box-one" @click="append('8')" value="8" />
        <input type="button" class="bg-two box-one" @click="append('9')" value="9" />
        <input type="button" class="bg-one box-one" @click="divide()" value="÷" />
      </div>

      <!-- row three -->
      <div class="flex">
        <input type="button" class="bg-two box-one" @click="append('4')" value="4" />
        <input type="button" class="bg-two box-one" @click="append('5')" value="5" />
        <input type="button" class="bg-two box-one" @click="append('6')" value="6" />
        <input type="button" class="bg-one box-one" @click="multiple()" value="x" />
      </div>

      <!-- row four -->
      <div class="flex">

        <input type="button" class="bg-two box-one" @click="append('1')" value="1" />
        <input type="button" class="bg-two box-one" @click="append('2')" value="2" />
        <input type="button" class="bg-two box-one" @click="append('3')" value="3" />
        <input type="button" class="bg-one box-one" @click="minus()" value="-" />
      </div>

      <!-- row five -->
      <div class="flex">
        <input type="button" class="bg-two box-one" @click="append('0')" value="0" />
        <input type="button" class="bg-two box-one" @click="dot" value="." />
        <input type="button" class="bg-two box-one" @click="equal()" value="=" />
        <input type="button" class="bg-one box-one" @click="plus()" value="+" />
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      display: '',
      operator: null,
      previous: null,
      operatorClick: false
    }
  }, methods: {
    clear() {
      this.display = ''
    }
    , append(number) {
      if (this.operatorClick) {
        this.display = ""
        this.operatorClick = false
      }
      this.display += number
    },
    dot() {
      if (!this.display.includes('.')) {
        this.append('.')
      }
    },
    setPrevious() {
      this.previous = this.display
      this.operatorClick = true
    }
    ,
    plus() {
      this.operator = (a, b) => a + b
      this.setPrevious()
    },
    minus() {
      this.operator = (a, b) => a - b
      this.setPrevious()
    },
    multiple() {
      this.operator = (a, b) => a * b
      this.setPrevious()
    },
    divide() {
      this.operator = (a, b) => a / b
      this.setPrevious()
    },
    equal() {
      this.display = this.operator(parseFloat(this.previous), parseFloat(this.display))
    }
  }
}
</script>

<style scoped>
.container {
  /* display: flex; */
  width: 100%;
  height: 600px;
}

.box-one {
  width: 100px;
  height: 100px;
  margin: 5px;
  cursor: pointer;
}

.box-two {
  width: 320px !important;
  /* height: 100px !important; */
  margin: 5px;
  text-align: center;
  cursor: pointer;
}

.bg-one {
  background-color: steelblue;
}

.bg-two {
  background-color: skyblue;
}

.flex {
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: center;
}

input[type="button"],
input[type="text"] {
  font-size: 25px;
  color: black;
  border: 1px solid black;
}

input[type="button"]:hover {
  background-color: darkblue;
  color: white;
  font-size: 40px;
  transform: translate(0, -7px);
}

div.display {
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 25px;
  color: black;
  border: 1px solid black;
}
</style>
