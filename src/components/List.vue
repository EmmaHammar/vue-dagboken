<template>
    <div>
      <h2>Sparade saker:</h2>
      <div v-for="item in items" :key="item.id" class="itemCard"> 
          <h3>{{item.title}}</h3>
          <p>{{item.date}}</p>
          <p>{{item.text}}</p>
      </div>
          
    </div>
</template>

<script>

export default {
    name: "List",
    props: {
        items: {
            type: Array,
        }
    },
    //behöver ej göra items o item i state data() för att jag inte vill modifiera dem, då räcker det att de är props
}
</script>

<style>
    .itemCard {
        border: 1px solid #333;
    }
</style>