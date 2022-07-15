<template>
  <div class="home">
    <FilterNav @filterValue="current = $event" :current="current"/>
    <div v-for="project in filteredProject" :key="project.id">
      <SingleProject
        :project="project"
        @delete="deleteProject"
        @complete="completeProject"
      />
    </div>
  </div>
</template>

<script>
import SingleProject from "../components/SingleProject";
import FilterNav from "../components/FilterNav";
// @ is an alias to /src

export default {
  name: "HomeView",
  components: {
    SingleProject,
    FilterNav,
  },
  data() {
    return {
      projects: [],
      current: "all",
    };
  },
  methods: {
    deleteProject(id) {
      this.projects = this.projects.filter((project) => {
        return project.id != id;
      });
    },
    completeProject(id) {
      let findProject = this.projects.find((project) => {
        return project.id === id;
      });
      findProject.complete = !findProject.complete;
    },
  },
  computed: {
    filteredProject() {
        if(this.current==="complete") {
            return this.projects.filter((p)=>{
                return p.complete
            })
        }
        else if (this.current==="ongoing") {
            return this.projects.filter((p)=>{
                return !p.complete
            })
        }
        return this.projects;
    }
  },
  mounted() {
    fetch("http://localhost:3000/projects")
      .then((response) => {
        return response.json();
      })
      .then((datas) => {
        this.projects = datas;
      })
      .catch((err) => {
        console.log(err.message);
      });
  },
};
</script>

<style>
h1 {
  margin: 10px;
}
</style>
