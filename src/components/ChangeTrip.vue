<template>
  <div class="add-form-container">
    <form action="" class="add-form" id="add-form">
      <label for="data">Data:</label><br />
      <input type="date" id="date" /><br />
      <label for="mezzo">Mezzo:</label><br />
      <input type="text" id="mezzo" /><br />
      <label for="coordinate">Coordinate:</label><br />
      <input type="text" id="coord" /><br />
      <label for="tappe">Tappe principali:</label><br />
      <input type="text" id="tappe" /><br /><br />
      <button type="submit" @click="modifyTrip()">Cerca</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "ModifyTrip",
  methods: {
    async modifyTrip() {
      let json = {
        data: "test",
        mezzo: "test",
        coordinate: ["test"],
        tappe: ["test"],
      };
      console.log("json: " + json);
      console.log("json.data " + json.data);

      let modifyform = document.getElementById("add-form");
      modifyform.onsubmit = async (e) => {
        e.preventDefault();
        await fetch("http://localhost:3000/trips", {
          method: "POST",
          headers: {
            Accept: "application/json",
            "Content-Type": "application/json",
          },
          body: json,
        });
      };
    },
  },
};
</script>
