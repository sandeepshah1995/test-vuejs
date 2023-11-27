<template>
  <div>
    <input type="url" v-model="userURL" placeholder="Enter URL" />
    <br />
    <button @click="fetchPreview">Preview URL</button>
    <br />
    <div v-if="previewData">
      <p>**Title:** {{ previewData.title }}</p>
      <p>**Description:** {{ previewData.description }}</p>
      <img
        v-if="previewData.image"
        :src="previewData.image"
        alt="Preview Image"
      />
      <a :href="userURL" target="_blank">{{ previewData.domain }}</a>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import cheerio from "cheerio";

export default {
  name: "UrlPreview",
  data() {
    return {
      userURL: "",
      previewData: null,
    };
  },
  methods: {
    async fetchPreview() {
      if (this.userURL) {
        try {
          const response = await axios.get(this.userURL);
          const $ = cheerio.load(response.data);

          const title = $("title").first().text();
          const description =
            $('meta[name="description"]').attr("content") || "";
          const image = $('meta[property="og:image"]').attr("content") || "";
          const domain = new URL(this.userURL).hostname;

          this.previewData = {
            title,
            description,
            image,
            domain,
          };
        } catch (error) {
          console.error("Error fetching preview:", error);
          this.previewData = null;
        }
      } else {
        this.previewData = null;
      }
    },
  },
};
</script>
