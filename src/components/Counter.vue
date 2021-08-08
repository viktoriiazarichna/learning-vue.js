<template>
  <div class="hello">
     {{ counter }}
    <br>
    <button
        :class="['bold', getClassName()]"
        @click="inc">inc</button>
    <button @click="$emit('handleDecClick')">dec</button>
  </div>
</template>

<script>
export default {
  props: {
    counter: {
      type: Number,
      required: true
    }
  },
    methods: {
      inc() {
        this.$emit('handleIncClick')
      },
      getClassName() {
        return this.counter > 0 ? 'isInced' : 'isDecked'
      }
    }
  }
</script>

<style scoped>
  .hello {
    background: #2c3e50;
    color: darkgrey;
  }

  .bold {
    font-weight: bold;
  }

  .isInced{
    color: green;
  }
  .isDecked{
    color: red;
  }
</style>