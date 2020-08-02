<template>
  <div class="app">
    <input type="text" v-model="display" class="app__display">
    <div class="panel app__panel ">
      <button
        v-for="(index, key) in 10"
        :key="key"
        @click="addNumber(key)"
      >
        {{key}}
      </button>
      <button @click="event('prompt')"  id="prompt">=</button>
    </div>
    <div class="operators">
      <button @click="event('addition')">+</button>
      <button @click="event('subtraction')">-</button>
      <button @click="event('division')">/</button>
      <button @click="event('multiplication')">*</button>
    </div>
  </div>
</template>

<script>


export default {
  name: 'App',
  data(){
    return {
      display: '',
      oneValue: '',
      lastEvent: ''
    }
  },
  methods: {
    addNumber(value){
      this.display += String(value)
    },
    event(e){
      if (!this.oneValue) {
        this.oneValue = this.display
        this.lastEvent = e
        this.display = ''
      } else {
        this[e]()
      }


    },
    prompt(){
      switch (this.lastEvent) {
        case "subtraction":
          this.display = String(Number(this.oneValue) - Number(this.display))
          this.oneValue = ''
          break
        case "addition":
          this.display = String(Number(this.oneValue) + Number(this.display))
          this.oneValue = ''
          break
        case "division":
          this.display = String(Number(this.oneValue) / Number(this.display))
          this.oneValue = ''
          break
        case "multiplication":
          this.display = String(Number(this.oneValue) * Number(this.display))
          this.oneValue = ''
          break
      }
    },
    subtraction(){
      this.display = String(Number(this.oneValue) - Number(this.display))
      this.oneValue = ''
    },
    addition(){
      this.display = String(Number(this.display) + Number(this.oneValue))
      this.oneValue = ''
    },
    division(){
      this.display = String(Number(this.oneValue) / Number(this.display))
      this.oneValue = ''
    },
    multiplication(){
      this.display = String(Number(this.display) * Number(this.oneValue))
      this.oneValue = ''
    }
  },
  components: {

  }
}
</script>

<style>
  .app {
    width: 320px;
    height: 480px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-template-rows: 60px 180px
  }
  #prompt {
    grid-column: 3/4;
  }
  .app__display {
    max-height: 60px;
    grid-column: 1/5;
  }

  .panel {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-column: 1/4;
  }

  .app__display {
    flex-grow: 1;
  }
  .operators {
    display: grid;
    grid-template-columns: 1fr;

  }

</style>
