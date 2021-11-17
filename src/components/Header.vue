<template>
  <header>
    <div class="header-container">
      <h1 class="text-danger">BOOLFlIX</h1>
      <div class="my-imput-group">
        <input type="text" class="" placeholder="Cerca un Film.." v-model="inputText">
        <div class="input-group-append">
         <button class="btn btn-primary" type="button" @click="addMovie">Button</button>
        </div>
      </div>

    </div>
  </header>
</template>

<script>

export default {
  name: "Header",
  data(){
    return{
      inputText: "",
    }
  },
  methods:{
    addMovie(){
      
    }
  }
}
</script>

<style lang="scss">
  .header-container{
    display: flex;
    align-items: center;
    justify-content: space-between;
    background-color: black;
    height: 80px;
    padding: 10px 20px;
  
    .my-imput-group{
      display: flex;
    }
  }

</style>