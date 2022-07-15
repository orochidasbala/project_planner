<template>
  <nav class="filternav">
    <div>
        <button @click="filterBy('all')" :class="{ activeall: current === 'all' }">
          projects
        </button>
        <button
          @click="filterBy('complete')"
          :class="{ activecomplete: current === 'complete' }"
        >
          completed
        </button>
        <button
          @click="filterBy('ongoing')"
          :class="{ activeongoing: current === 'ongoing' }"
        >
          ongoing
        </button>
    </div>
  </nav>
</template>

<script>
export default {
  props: ["current"],
  methods: {
    filterBy(value) {
      this.$emit("filterValue", value);
    },
  },
};
</script>

<style scoped>
div{ 
    height: 50px;
    padding: 10px 0;
}
button {
    color: rgb(92, 92, 92);
    background: none;
    border: none;
    margin: 10px;
    padding: 20px 2px 5px 2px;
    font-size: 12px;
    text-transform: uppercase;
    letter-spacing: 1px;
    transition: 0.5s ;
    text-align: left;
}
button.activeall {
    color: rgb(5, 121, 253);
    font-size: 12px;
}
button.activecomplete {
    color: rgb(0, 185, 62);
    font-size: 12px;
}
button.activeongoing {
    color: crimson;
    font-size: 12px;
}
</style>