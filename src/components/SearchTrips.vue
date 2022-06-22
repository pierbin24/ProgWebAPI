<template>
  <!-- sistemo brbrbrbrbrbbrbrbrbrbrbrbrbrbrbrbrbrbrbrbrbrbr -->
  <div class="add-form-container">
    <form action="" class="add-form" id="add-form">
      <legend>Siti per webmaster</legend>
      <select name="siti">
        <option value="http://www.html.it" selected="selected">
          www.html.it
        </option>
        <option value="http://freephp.html.it">frephp.html.it</option>
        <option value="http://freasp.html.it">freasp.html.it</option>
      </select>

      <label for="data">Data:</label><br />
      <input type="date" id="date" /><br />
      <label for="mezzo">Mezzo:</label><br />
      <input type="text" id="mezzo" /><br />
      <label for="coordinate">Coordinate:</label><br />
      <input type="text" id="coord" /><br />
      <label for="tappe">Tappe principali:</label><br />
      <input type="text" id="tappe" /><br /><br />
      <button type="submit" @click="addTrip()">Add</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "AddTrip",
  methods: {
    async addTrip() {
      var json;
      document.getElementById("add-form", function () {
        console.log(this.dataset.data);
        json = JSON.stringify({
          data: this.dataset.data,
          mezzo: this.dataset.mezzo,
          coordinate: this.dataset.coordinate,
          tappe: this.dataset.tappe,
        });
      });

      let addform = document.getElementById("add-form");

      console.log(json);
      console.log("ci sto dentro");
      addform.onsubmit = async (e) => {
        e.preventDefault();
        console.log("ci sto dentro");
        await fetch("http://localhost:3000/trips", {
          method: "POST",
          mode: "no-",
          headers: {
            "Content-Type": "application/json",
            // 'Content-Type': 'application/x-www-form-urlencoded',
          },
          body: json,
        });
      };
    },
  },
};
</script>

<style></style>
