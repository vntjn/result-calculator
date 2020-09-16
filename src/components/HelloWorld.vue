<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <br />
    <br />
    <div>
      <h3>ऑनलाइन एक्जाम में प्राप्त मार्क्स</h3>
      <input type="number" step=".01" v-model="onlineExamMarks" min="0" max="100" />
      <br />
      <br />
      <br />
      <h3>5th sem का SGPA</h3>
      <input type="number" step=".01" v-model="SGPA5thSem" min="0" max="10" />
      <br />
      <br />
      <br />
      <h3>फ़ाइनल थियरि मार्क्स</h3>
      {{ finalTheoryMarks }}
      <br />
      <br />
      <br />
      <h3>थियोरी रिज़ल्ट</h3>
      <span :style="resultColor">
        <b>{{ theoryResult }}</b>
      </span>
    </div>
    <div class="footer">&#169; Designed and created by Vinti Jain</div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      msg:
        "पोलिटेकनिक के 6th sem मे ऑनलाइन परीक्षा का रिज़ल्ट (ग्रेडिंग प्रणाली) जानने के लिए पूछी गई जानकारी को उसके नीचे वाले बक्से मे भरने पर रिज़ल्ट बताएगा।",
      onlineExamMarks: null,
      SGPA5thSem: null,
    };
  },
  computed: {
    finalTheoryMarks() {
      if (this.onlineExamMarks && this.SGPA5thSem) {
        return this.onlineExamMarks >= 0 &&
          this.onlineExamMarks <= 100 &&
          this.SGPA5thSem >= 0 &&
          this.SGPA5thSem <= 10
          ? this.onlineExamMarks / 2 + (7 * this.SGPA5thSem) / 2
          : "सही भरें";
      } else {
        return "दोनों बॉक्स भरें";
      }
    },
    theoryResult() {
      return this.finalTheoryMarks === "सही भरें"
        ? "सही भरें"
        : this.finalTheoryMarks === "दोनों बॉक्स भरें"
        ? "दोनों बॉक्स भरें"
        : this.finalTheoryMarks >= 22
        ? "PASS"
        : "FAIL";
    },
    resultColor() {
      return this.theoryResult === "PASS" ? "color: green" : "color: red";
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.footer {
  height: 15px;
  position: fixed;
  bottom: 0;
  background-color: white;
  font-size: 12px;
}
</style>
