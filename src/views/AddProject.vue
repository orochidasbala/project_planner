<template>
  <div class="formStyle">
    <div class="header">Add Project</div>
    <div>
      <form @submit.prevent="addProject">
        <div>
          <label>Project Title</label>
          <input type="text" v-model="title" />
        </div>
        <div>
          <label>Project Details</label>
          <textarea rows="5" v-model="detail"></textarea>
        </div>
        <div><button>Create Project</button></div>
      </form>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      title: "",
      detail: "",
    };
  },
  methods: {
    addProject() {
      fetch("http://localhost:3000/projects", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          project: this.title,
          details: this.detail,
          complete: false,
        }),
      })
        .then(() => {
          this.$router.push("/");
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>
<style scoped>
.formStyle {
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 15px;
  padding: 40px;
  margin-top: 10px;
  background-color: rgba(199, 199, 199, 0.432);
  display: inline-block;
  max-width: auto;
}
.header {
  display: flex;
  justify-content: center;
  margin-bottom: 40px;
  font-family: arial;
  text-transform: uppercase;
  font-weight: 900;
  font-size: 20px;
  letter-spacing: 2px;
}
label {
  display: block;
  text-transform: uppercase;
  font-size: 12px;
  color: grey;
  margin: 10px 0px;
  font-family: arial;
  font-weight: bold;
  letter-spacing: 1px;
}
input,
textarea {
  background-color: #fff;
  border: none;
  color: rgb(104, 104, 104);
  border-radius: 6px;
  padding: 12px;
  width: 526px;
  font-size: 14px;
  font-family: monospace;
}
button {
  border: none;
  background-color: rgb(192, 100, 228);
  margin-top: 20px;
  border-radius: 8px;
  padding: 14px 0;
  color: white;
  width: 550px;
  font-family: arial;
  font-weight: bold;
}
</style>