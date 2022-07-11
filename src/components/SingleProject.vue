<template>
    <div class="card" :class="{comp:project.complete}">
        <div class="title">
            <div class="flexing">
				<div>
					<h3 @click="Details">{{ project.project }}</h3>
				</div>
				<div>
					<span class="fa-solid fa-trash-can" @click="deleteProject"></span>
					<router-link :to="{name:'editProject', params:{id:project.id}}">
                        <span class="fa-solid fa-pen"></span>
                    </router-link>
					<span class="fa-solid fa-check" @click="completeProject"></span>
				</div>
			</div>
        </div>
        <div class="detail" v-if="showDetails">
            <p> {{ project.details }} <hr> Lorem ipsum dolor sit amet consectetur adipisicing elit. Quae doloremque ducimus quaerat reiciendis nesciunt possimus dolores sint dolor aperiam exercitationem
			</p>
        </div>
    </div>
</template>


<script>
export default {
  props: ["project"],
  data() {
    return {
      showDetails: false,
      api: "http://localhost:3000/projects/",
    };
  },
  methods: {
    Details() {
      this.showDetails = !this.showDetails;
    },
    deleteProject() {
      let deleteApi = this.api + this.project.id;
      fetch(deleteApi, { method: "DELETE" })
        .then(() => {
          this.$emit("delete", this.project.id);
        })
        .catch((err) => {
          console.log(err.message);
        });
    },
    completeProject() {
      let completeProjectRoute = this.api + this.project.id;
      fetch(completeProjectRoute, {
        method: "PATCH",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          complete: !this.project.complete,
        }),
      })
        .then(() => {
          this.$emit("complete", this.project.id);
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>


<style>
.flexing {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.card {
  background-color: #ddd;
  margin: 15px 10px;
  border-radius: 5px;
  border-left: 5px solid crimson;
}
.comp {
  border-left: 6px solid rgb(0, 137, 172);
}
.title {
  background-color: rgb(192, 100, 228);
  padding: 10px 20px;
  border-radius: 0 7px 7px 0;
}
span {
  margin-left: 10px;
  color: #ddd;
}
span:hover {
  cursor: pointer;
  color: #bbb;
}
.detail {
  padding: 20px 20px;
  border: none;
}
h3 {
  color: rgb(255, 255, 255);
  text-transform: uppercase;
  letter-spacing: 2px;
  cursor: pointer;
  font-size: 15px;
}
hr {
  color: white;
}
</style>