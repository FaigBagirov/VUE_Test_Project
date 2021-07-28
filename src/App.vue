
<template>
<!-- This template is inserted into div with "#app" id, Except the teleports-->

  <div>
    <h1>{{title}}</h1>

    <!-- //To access a "ref" attribute I need to write one -->
    <input type="text" ref="someRefName">
    <!-- adding 'click' event listener to a button  -->
    <button @click="handleClick" >click</button>
  </div>

  <!-- 1e) Teleport: I can cut this part of template and paste anywhere inside the index.html -->
  <!-- choose the destination by "div"'s "class" or "id" selector-->
  <teleport to="#teleportDest" v-if="showModal">
    <!-- 3a)Add a component: use it by inserting the component in html as a tag as many times as you want -->
    <!-- 2c)Add custom event: attach action to the event as if it were built in event like "click" -->
    <Modal class="modal" theme="sale" @closeEvent="toggleModal" someArgument="Value of the argument" :someOtherArgument="bindedVariable" /> <!-- 1b)Pass argument to a component: write it here as an attribute -->
  </teleport>

  <div v-if="showSlotModal">
    <!-- 1d) Slot: To pass  template to a component use component as openening and closing tags  <Modal></Modal> -->
    <!-- 2d) Slot: then paste whatever you want between these tags -->
    <Modal class="slotModal" theme="" @closeEvent="toggleSlotModal" someArgument="Value of the argument" :someOtherArgument="bindedVariable" >
      
      <!--4d)Slot: this is default slot -->
      <button>This is default slot</button>
      
      <!-- 5d) Slot: This is named slot it is shown only in slots with same name  -->
      <template v-slot:someSlotName>
        <button> This is named slot</button>
      </template>
    </Modal>
  </div>

  <!-- event modifier: "click.shift" trigger only on "shift"+"click" -->
  <button class="showTheModal" @click.shift="toggleModal"> Shift+click to show the modal </button>
  <button class="showTheSlotModal" @click ="toggleSlotModal">Click to show modal with slot </button>

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
      showSlotModal: false,
    }
  },
  methods: {
    handleClick() {
      //instead of queryselector (it doesn't work here) I can access elements by "ref" attribute
      console.log(this.$refs.someRefName) 
      this.$refs.someRefName.classList.add('active');
      this.$refs.someRefName.focus(); //this will put focus on "input" element when I click the button
    },
    toggleModal (somePassedVar){//arguments passed with emit event are automatically available like funtion argument 
      console.log(somePassedVar);
      this.showModal = !this.showModal;
    },
    toggleSlotModal (){
      this.showSlotModal = !this.showSlotModal;
    }
  },

}
</script>


<style>
/* these styles are global as well as all other styles inside components*/
/* to make a style scoped its better to adress them to some general class name */
/* never use "scoped" attribute in main App.vue file */
#app{
  text-align: center;
}
.showTheModal{
  margin-top: 50px;
}
.showTheSlotModal{
  margin-left: 20px;
}
</style>
