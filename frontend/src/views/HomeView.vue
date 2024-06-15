/* eslint-disable */
<template>
  <div>
    <v-container>
      <h1 class="mb-5">Job Board</h1>
      <div v-for="job in jobs" :key="job.pk">
        <h2>
          <router-link
            :to="{ name: 'job', params: { id: job.id } }"
            class="job-link"
            >{{ job.company_name }}
          </router-link>
        </h2>
        <p>{{ job.job_title }}</p>
        <hr />
      </div>
      <div class="my-4">
        <p v-show="loadingJobs">...loading...</p>
        <v-btn v-show="next" @click="getJobs" color="blue">Load More</v-btn>
      </div>
    </v-container>
  </div>
</template>

<script>
// @ is an alias to /src
// import router from "@/router/index.js";
import { apiService } from "../common/api.service.js";

export default {
  name: "HomeView",
  data() {
    return {
      jobs: [],
      loadingJobs: false,
      next: null,
    };
  },
  methods: {
    getJobs() {
      // endpointは/が必要
      let endpoint = "api/jobs/";
      if (this.next) {
        endpoint = this.next;
      }
      this.loadingJobs = true;
      apiService(endpoint).then((data) => {
        this.jobs.push(...data.results);
        this.loadingJobs = false;
        if (data.next) {
          this.next = data.next;
        } else {
          this.next = null;
        }
      });
      console.log(this.jobs);
    },
  },
  created() {
    this.getJobs();
    // 画面タイトル
    document.title = "Job Board";
    // console.log("this.created()");
  },
};
</script>

<style scoped>
.job-link {
  font-weight: bold;
  color: black;
  text-decoration: none;
}
.job-link:hover {
  color: rgb(73, 120, 120);
}
</style>
