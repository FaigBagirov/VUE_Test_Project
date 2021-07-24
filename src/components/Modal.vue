<template>
  <div class="backdrop">
    <div class="modal">
      <h1>Modal Title and {{someArgument}}</h1>
      <p>modal content and {{someOtherArgument}}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ['someArgument', 'someOtherArgument'] // 2b)Pass argument to a component: Specify it inside the "props" object
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only IT AFFECTS PERFORMANCE SLIGHTLY (it works with datasets)-->
<style scoped> 
  .modal{
    width: 400px;
    padding: 20px;
    margin: 100px auto; /*vertically "100px", horizontally centrally aligned*/
    background: white;
    border-radius: 10px;
  }
  .backdrop{
    top:0;
    position: fixed;
    background: rgba(0,0,0,0.5);
    width: 100%;
    height: 100%;
  }
  .modal h1{
    color: #03cfb4;
    border: none;
    padding: none;
  }

/* override global styles by respecifying them  */
  .modal p {
    font-style: normal;
  }
</style>
