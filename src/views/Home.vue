<template>
  <div class="main">
    <v-card fluid class="mx-auto" max-width="500px" style="margin: 30px 0px">
      <v-img class="white--text align-end" height="300px" :src="img.img" :alt="img.alt">
        <v-card-title>Harry Potter and the Deathly Hallows Part 2</v-card-title>
      </v-img>
      <!-- Show this before processing -->
      <div v-if="process==0">
        <v-card-subtitle class="pb-0 pl-5 pr-5">
          <v-text-field
            v-model="userComment"
            :loading="loading_review_classification"
            label="Type your Review here"
            append-icon="send"
            :disabled="loading_review_classification ? true : false"
            @click:append="processReview"
          ></v-text-field>
        </v-card-subtitle>

        <v-card-subtitle class="pb-2 pl-5 pr-5" style="margin-bottom: 10px;">
          <span>Hint: Longer reviews tend to have higher accuracy.</span>
        </v-card-subtitle>
      </div>

      <!-- Show this after processing -->
      <div v-if="process==1">
        <div class="d-flex flex-column mb-6">
          <v-card-subtitle class="pl-5">
            <span>
              Very Good!! Your review was classified as
              <strong>{{ usersSentiment }}</strong>!!!
            </span>
          </v-card-subtitle>
          <v-select
            :items="['Positive', 'Negative']"
            label="What was yout review sentiment?"
            class="pl-5 pr-5"
            prepend-icon="mdi-account-question-outline"
            v-model="usersSentimentFeedback"
          ></v-select>
        </div>
        <div class="text-center mb-5">
          <v-btn color="green lighten-3" @click="sendFeedback">Send Feedback</v-btn>
        </div>
      </div>

      <!-- Show this at the end of the process -->
      <div v-if="process==2">
        <v-card-subtitle class="pl-5">
          <span>Thank you!!!</span>
        </v-card-subtitle>
        <div class="text-center mb-5">
          <v-btn color="green lighten-3" @click="goBack">Go Back</v-btn>
        </div>
      </div>
    </v-card>
  </div>
</template>

<script>
const img = require("./../assets/HP7-2.jpg");

export default {
  components: {},

  data: () => ({
    userComment: "",
    usersSentiment: "",
    usersSentimentFeedback: "",
    img: {
      img: img,
      alt: "Harry Potter and the Deathly Hallows Part 2"
    },
    process: 0,
    loading_review_classification: false
  }),

  methods: {
    async processReview() {
      this.loading_review_classification = true;

      const translate = {
        neg: "Negative",
        pos: "Positive"
      };

      await this.axios
        .post("/movie-review-predict", { review: this.userComment })
        .then(response => {
          this.usersSentiment = translate[response.data.classification];
          this.process = 1;
        });
    },

    sendFeedback() {
      console.log(this.usersSentimentFeedback);
      this.process = 2;
    },

    goBack() {
      this.process = 0;
      this.loading_review_classification = false;
      this.userComment = "";
    }
  }
};
</script>

<style scoped>
.main {
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>


