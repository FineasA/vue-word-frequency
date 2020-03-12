<template>
  <div class="container">
    <div class="row justify-content-center">
      <h4>Word Frequency Counter</h4>
    </div>
    <hr />
    <div class="row justify-content-center">
      <textarea
        class="userTextArea"
        name="userText"
        cols="30"
        rows="10"
        v-model="userText"
      ></textarea>
    </div>
    <br />
    <div class="row justify-content-center">
      <button @click="getWordData" class="btn btn-primary">Translate</button>
    </div>
    <br />
    <div
      class="row"
      style="margin: 0 auto; max-width: 250px; text-align: center"
      v-if="translated"
    >
      <b-table striped hover :items="wordsArr"></b-table>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      userText: "A dinosaur is a chicken but a baby dinosaur",
      userTextArr: [],
      words: [],
      set: {
        word: "",
        wordFrequency: 0
      },
      wordsArr: [],
      translated: false
    };
  },
  methods: {
    getWordData() {
      this.userText = this.userText.toLowerCase();
      this.userTextArr = this.userText.split(" ");
      this.countWords();

      this.words = Object.entries(this.words);
      //destructure array
      for (const [word, count] of this.words) {
        console.log(`There are ${count} ${word}`);
        this.set.word = word;
        this.set.wordFrequency = count;
        this.wordsArr.push(this.set);
        this.set = {};
      }
      this.translated = true;
      console.log(this.wordsArr);
    },
    countWords() {
      this.userTextArr.reduce((count, word) => {
        count[word] = (count[word] || 0) + 1;
        this.words = count;
        return count;
      }, {});
    }
  }
};
</script>

<style>
.userTextArea:focus {
  outline: none;
}
</style>
