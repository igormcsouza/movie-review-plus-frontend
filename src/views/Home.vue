<template>
  <div class="main">
    <v-card fluid class="mx-auto" max-width="500px" style="margin: 30px 0px">
      <v-img class="white--text align-end" height="300px" :src="img.img" :alt="img.alt">
        <v-card-title>Harry Potter and the Deathly Hallows Part 2</v-card-title>
      </v-img>
      <!-- Show this before processing -->
      <div v-if="getting_review">
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
      <div v-else>
        <div class="d-flex flex-column mb-6">
          <v-card-subtitle class="pl-5">
            <span>
              Very Good!! Your review as
              <strong>POSITIVE</strong>!!!
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
        <div class="text-center mb-2">
          <v-btn text color="green lighten-3" @click="sendFeedback">Send Feedback</v-btn>
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
    usersSentimentFeedback: "",
    img: {
      img: img,
      alt: "Harry Potter and the Deathly Hallows Part 2"
    },
    loading_review_classification: false,
    getting_review: true
  }),

  methods: {
    processReview() {
      this.loading_review_classification = true;

      console.log(this.userComment);

      setTimeout(() => (this.getting_review = false), 3000);
    },

    sendFeedback() {
      console.log(this.usersSentimentFeedback);
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


