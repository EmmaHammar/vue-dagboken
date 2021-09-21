<template>
  <div>
      <form @submit="onSubmit">
          <input type="text" placeholder="Rubrik" id="title"><br />
          <input type="date" placeholder="Datum" id="date"><br />
          <input type="text" placeholder="Text" id="text"><br />
          <button>Spara</button>
      </form>
  </div>
</template>

<script>

export default {
    name: "Form",
    //behöver ej göra items o item i state data() för att jag inte vill modifiera dem, då räcker det att de är props
    methods: {
        onSubmit(evt) {
            evt.preventDefault();
            // console.log("klick saveBtn", evt.target.title.value);

            //spara lS: kalla på saveData från App.vue o skicka med evt:
            this.$emit("saveData", evt)
        }
    }

}
</script>

<style>

</style>