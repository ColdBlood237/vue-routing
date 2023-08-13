<template>
  <div v-if="job">
    <h1>{{ job.title }}</h1>
    <p>The job id is {{ id }}</p>
    <p>{{ job.details }}</p>
  </div>
  <div v-else>
    <p>Loading job details...</p>
  </div>
</template>

<script>
export default {
  props: ["id"],
  data() {
    return {
      job: null,
    };
  },
  methods: {
    async fetchData() {
      try {
        const response = await fetch("http://localhost:3000/jobs/" + this.id);
        const data = await response.json();
        this.job = data;
      } catch (err) {
        console.log(err.message);
      }
    },
  },
  mounted() {
    this.fetchData();
  },
};
</script>

<style></style>
