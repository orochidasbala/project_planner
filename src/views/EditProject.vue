<template>
	<div class="formStyle">
    <div class="header">Edit Project</div>
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
        <div><button @click="updateProject">Update Project</button></div>
      </form>
    </div>
  </div>
</template>
<script>
export default {
	props: ['id'],
	data(){
		return {
			title: "",
			detail: ""
		}
	},
	mounted(){
		fetch("http://localhost:3000/projects/"+this.id)
		.then((response)=>{
			return response.json()
		})
		.then((datas)=> {
			this.title = datas.project,
			this.detail = datas.details
		})
		.catch((err)=>{
			console.log(err);
		})
	},
	methods: {
		updateProject() {
			fetch("http://localhost:3000/projects/"+this.id, {
				method:"PATCH",
				headers: {
					"Content-Type": "application/json"
				},
				body:JSON.stringify({
					project: this.title,
					details: this.detail
				})
			})
			.then(()=>{
				this.$router.push('/')
			})
			.catch((err)=> {
				console.log(err)
			})
		}
	}
}
</script>
<style>
	
</style>