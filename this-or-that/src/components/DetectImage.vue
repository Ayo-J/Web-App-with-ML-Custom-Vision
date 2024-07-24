<template>
  <div>
    <h1>{{ msg }}</h1>
    <div>
      <img class="image" ref="img" :src="require('../assets/images/' + getImgIndex + '.jpg')" />
    </div>
    <div>
      <button class="button" @click="next()" :disabled="disable">Next</button>
    </div>
    <div v-for="pred in predictions" :key="pred.index">
      {{ pred.label }}: {{ pred.probability.toFixed(0) + '%' }}
    </div>
    <div v-if="!predictions.length">hmm.....</div>
  </div>
</template>

<script>
export default {
  name: 'DetectImage',
  props: {
    msg: String,
  },
  data() {
    return {
      image: 0,
      numImages: 16,
      predictions: [],
    };
  },
  computed: {
    getImgIndex() {
      return this.image.toString();
    },
    disable() {
      return this.image === this.numImages;
    },
  },
  methods: {
    next() {
      this.image++;
      this.predictions = [];
      setTimeout(this.predict, 500);
    },
    predict() {
      // Prediction logic will go here later
    },
  },
};
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
.image {
  min-height: 300px;
  max-height: 300px;
  max-width: 100%;
}
.button {
  width: 200px;
  height: 50px;
  border-radius: 5px;
  background-color: blueviolet;
  color: white;
  font-size: 20pt;
  margin: 10px;
}
.button:disabled,
.button[disabled] {
  border: 1px solid #999999;
  background-color: #cccccc;
  color: #666666;
}
</style>
