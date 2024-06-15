/* eslint-disable */
<template>
  <div>
    <v-container>
      <h2 class="mb-5">{{ job.company_name }}</h2>
      <p>職業: {{ job.job_title }}</p>
      <p>内容: {{ job.job_description }}</p>
      <p>給料: {{ job.salary }}</p>
      <p>都道府県: {{ job.prefectures }}</p>
      <p>市町村: {{ job.city }}</p>
      <v-btn
        color="blue"
        class="mr-2"
        :to="{ name: 'editor', params: { id: job.id } }"
        >編集
      </v-btn>
      <v-btn color="red" @click="deleteJobData">削除</v-btn>
    </v-container>
  </div>
</template>

<script>
import { apiService } from "../common/api.service.js";

export default {
  name: "JobView",
  props: {
    id: {
      type: Number,
      required: true,
    },
  },
  data() {
    return {
      job: {},
    };
  },
  methods: {
    setPageTitle(title) {
      document.title = title;
    },
    getJobData() {
      console.log("beforegetdata");
      let endpoint = `/api/jobs/${this.id}/`;
      apiService(endpoint).then((data) => {
        this.job = data;
        console.log(data);
        console.log("data");
        this.setPageTitle(data.company_name);
      });
    },
    deleteJobData() {
      console.log("deleteJob");
      // attention：先頭に/つける
      let endpoint = `/api/jobs/${this.id}/`;
      let method = "DELETE";
      apiService(endpoint, method).then(() => {
        this.$router.push({ name: "home" });
      });
    },
  },
  created() {
    this.getJobData();
    console.log("this.getJobData()");
  },
};
</script>
