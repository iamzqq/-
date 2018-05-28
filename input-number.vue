<template>
  <div>
    <div class="inputWrap">
      <span class="minus icon-minus" v-on:click="minus()" :class="{nouse:currentnumber==min}">－</span>
      <input type="text" v-model="currentnumber">
      <span class="addicon icon-add" v-on:click="add()" :class="{nouse:currentnumber==max}">＋</span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    step: {
      type: Number,
      default: 1
    },
    max: {
      type: Number,
      default: Infinity
    },
    min: {
      type: Number,
      default: 1
    },
    value: {
      default: 1
    }
  },
  data () {
    return {
      currentnumber: ''
    }
  },
  mounted() {
    this.currentnumber = this.value
  },
  methods: {
    setnewval(oldval, newval) {
      this.currentnumber = newval
      this.$emit('change', oldval, newval)
    },
    add() {
      if (this.currentnumber >= this.max) {
        return;
      }
      let oldval = this.currentnumber;
      let newval = this.currentnumber + this.step;
      this.setnewval(oldval, newval)
    },
    minus() {
      if (this.currentnumber <= this.min) {
        return;
      }
      let oldval = this.currentnumber;
      let newval = this.currentnumber - this.step;
      this.setnewval(oldval, newval)
    }
  }
}
</script>

<style scoped>
  .inputWrap {
    position: relative;
    padding: 0 35px;
    width: 105px;
  }

  .addicon, .minus {
    width: 30px;
    height: 30px;
    display: inline-block;
    position: absolute;
    padding: 5px;
    background-color: #f0f0f0;
    font-size: 18px;
    color: #333;
  }

  .minus {
	user-select:no-select;
    left: 0;
    top: 0;
  }

  .addicon {
    right: 0;
    top: 0;
  }

  input {
    width: 35px;
    height: 30px;
    text-align: center
  }
  .nouse{color: #aaa}
</style>
