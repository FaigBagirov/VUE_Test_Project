<template>
  <div>
    <h1>{{title}}</h1>

    <!-- //To access a "ref" attribute I need to write one -->
    <input type="text" ref="someRefName">
    <!-- adding 'click' event listener to a button  -->
    <button @click="handleClick" >click</button>
  </div>

  <div v-if="showModal">
    <!-- 3a)Add a component: use it by inserting the component in html as a tag as many times as you want -->
    <!-- 2c)Add custom event: attach action to the event as if it were built in event like "click" -->
    <Modal @closeEvent="toggleModal" someArgument="Value of the argument" :someOtherArgument="bindedVariable" theme="sale"/> <!-- 1b)Pass argument to a component: write it here as an attribute -->
  </div>

  <!-- event modifier: "click.shift" trigger only on "shift"+"click" -->
  <button class="showTheModal" @click.shift="toggleModal"> Show the modal </button>
</template>

<script>

// 1a)add a component: import the component file like this
  // never name components as regular html tags like "div", "footer", etc. 
 import Modal from './components/Modal.vue' //comonents can be placed anywhere inside "src" folder

export default {
  name: 'App',
  components: {
      Modal //2a)add a component: register the component
  },
  data(){
    return {
      title: "First app",
      bindedVariable: "Some  binded data passed as argument",
      showModal: false,
    }
  },
  methods: {
    handleClick() {
      //instead of queryselector (it doesn't work here) I can access elements by "ref" attribute
      console.log(this.$refs.someRefName) 
      this.$refs.someRefName.classList.add('active');
      this.$refs.someRefName.focus(); //this will put focus on "input" element when I click the button
    },
    toggleModal (){
      this.showModal = !this.showModal;
    }
  },

}
</script>


<style>
/* these styles are global as well as all other styles inside components*/
/* to make a style scoped its better to adress them to some general class name */
/* never use "scoped" attribute in main App.vue file */
.showTheModal{
  margin-top: 50px;
}
</style>
