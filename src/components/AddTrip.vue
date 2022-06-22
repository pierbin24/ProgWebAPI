<template>
  <!-- sistemo brbrbrbrbrbbrbrbrbrbrbrbrbrbrbrbrbrbrbrbrbrbr -->
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
      <button type="submit" @click="addTrip()">Add</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "AddTrip",
  methods: {
    async addTrip() {
      //  formElem.onsubmit = async (e) => {
      //     e.preventDefault();

      //     let response = await fetch('/article/formdata/post/user', {
      //       method: 'POST',
      //       body: new FormData(formElem)
      //     });
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
          mode: "no-cors",
          headers: {
            "Content-Type": "application/json",

            // 'Content-Type': 'application/x-www-form-urlencoded',
          },
          body: json,
        });
      };

      // await document
      //   .getElementById("add-form")
      //   .addEventListener("submit", function (e) {
      //     e.preventDefault();
      //     const addForm = document.getElementById("add-form");
      //     let formData = new FormData(addForm);
      //     let form = JSON.stringify(formData);
      //     console.log(JSON.stringify(formData));
      //     console.log("ci sto dentro");
      //     // let formData = new FormData(this);
      //     // var object = {};
      //     // formData.forEach((value, key) => (object[key] = value));
      //     // var json = JSON.stringify(object);
      //     fetch("http://localhost:3000/trips", {
      //       method: "POST",
      //       headers: {
      //         "Content-Type": "application/json",
      //         // 'Content-Type': 'application/x-www-form-urlencoded',
      //       },
      //       body: form,
      //     });
      //   });
    },
  },
  // mounted() {
  //   this.addTrip();
  // },
};
</script>

<style></style>
