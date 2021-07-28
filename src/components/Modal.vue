<template>
<!-- event modifier: trigger only if clicked on parent div not it's children -->
  <div class="backdrop" @click.self="closeModal">
    
    <!-- "{sale: theme === 'sale'}" means Add class name 'sale' if :the statement is true  -->
    <div class="modal" :class="{sale: theme === 'sale'}">
      
      <h1>Modal Title - {{someArgument}}</h1>
      <p>modal content - {{someOtherArgument}}</p>
      
      <!-- 6d) Slot: write the name attribute to pass named slot (template) -->
      <slot name="someSlotName"></slot>

      <!-- 3d) Slot: Just write <slot></slot> anywhere you want to paste the unnamed (default) slot (template) -->
      <slot>Default content when no slot is passed to a component</slot>
    </div>
  </div>
</template>

<script>
export default {
  props: ['someArgument', 'someOtherArgument', 'theme'], // 2b)Pass argument to a component: Specify it inside the "props" object
  data(){
    return{
      someTimer: null,
      someCounter: 0,
    }
  },
  methods: {
    closeModal () {
      //1c) Add custom event: use "$emit()" function
      //works same as built in events "click", "change", etc.
      this.$emit('closeEvent', this.someCounter); //you can pass variablse along with "emit" event
    },
    // read about startTimer and setInterval in devs mozilla com
    startTimer(){
      this.someTimer = setInterval(()=>{
        this.someCounter += 10; 
      }, 10)//will make "startTimer" to trigger every 10 milliseconds 
    },
    //stops selected timer 
    stopTimer() {
      clearInterval(this.someTimer);
    }
  },
  // this hook triggers when this component is being mounted but before it's being shown on web page
  mounted(){
    // do something if you need it
  },
  // this trigger exactly when the component is updated
  updated(){

  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only IT AFFECTS PERFORMANCE SLIGHTLY (it works with datasets)-->
<style scoped> 
  .modal{
    width: 400px;
    padding: 20px;
    margin: 100px auto; /*vertically "100px", horizontally centrally aligned*/
    background: black;
    border-radius: 10px;
  }
  .backdrop{
    top:0;
    position: fixed;
    background: rgba(0,0,0,0.5);
    width: 100%;
    height: 100%;
  }
  .modal{
    color: #03cfb4;
    border: none;
    padding: none;
  }

/* override global styles by respecifying them  */
  .modal p {
    font-style: normal;
  }

  /*Select element with two classes ".oneClass.otherClass" without spaces between them*/
  /*Select CHILD element: ".parentClass childElementClass" there's space between them.*/
  /*exmpl. I could select same element by it's parent: ".backdrop .sale" */
  .modal.sale{
    background: crimson;
    color: white;
  }

  .modal button{
    color: white;
    border-radius: 4px;
    margin: 10px
  }
</style>  
