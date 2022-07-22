<template>
 <div class="container">
  <div class="content">
    <div class="answers" v-if="hasEnd">
      <h1 class="passed" v-if="corrects.length >= 7" :class="{active : corrects.length >= 7}">Sizning to'gri javoblaringiz soni : {{corrects.length}}</h1>
      <h1 class="failed" v-else-if="corrects.length < 7" :class="{active : corrects.length < 7}">Sizning to'gri javoblaringiz soni : {{corrects.length}}</h1>
      <button @click="tryAgain()" class="btn-end">Qaytadan boshlash</button>
    </div>
    <div class="tabs">
    <div class="top">
      <div class="btn-question">
        <span @click="currentIndex=i" :class="{active: currentIndex==i}" class="btn" v-for="(e,i) in datas" :key="i">
      {{i+1}}
      </span>
      </div>
      <button v-if="!hasEnd" @click="check()" class="btn-end">Yakunlash</button>
    </div>
    <test-comp :hasEnd="hasEnd" :ref="'testComp'" v-for="(element,index) in renderQuestions" :key="element.id" :element="element" :index="index" :currentIndex="currentIndex"></test-comp>
    </div>
  </div>
 </div>
</template>
<script>
import TestComp from "./components/TestComp.vue"
import myJson from "../src/assets/json/datas.json"

export default {
  components : {
    TestComp
  },
  data() {
    return {
      currentIndex: 0,
      datas: myJson,
      answers : [],
      hasEnd: false,
      corrects: [],
    }
  },
  methods: {
    check() {
      if(confirm("Imtihonni haqiqatdan ham yakunlamoqchimisiz?")) {
        this.hasEnd = true;
        this.currentIndex = 0
        this.corrects = this.$refs.testComp[0]?.answers.filter(el => el==true);
      }
    },
    tryAgain() {
        this.hasEnd = false;
        this.currentIndex = 0;

    },
    shuffle(array) {
      array.sort(() => Math.random() - 0.5);
}
  },
  watch: {
    datas: {
      deep: true,
      handler() {
        this.renderQuestions
      }
    }
  },
  computed: {
    renderQuestions() {
      return this.datas.filter(el => el.index == this.currentIndex);
    },
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  user-select: none;
}
body {
  font-family: "Gilroy";
}
.container {
  width: 1100px;
  margin: 0 auto;
}
.content {
  width: 900px;
  margin: 0 auto;
  background: #f2f6ff;
  margin-top: 1rem;
}
.question {
  display: flex;
  margin-top: 2rem;
  font-size: 24px;
  margin-bottom: 1rem;
}
.question span {
  margin-right: 5px;
}
.btn {
  background: #fff;
  border: 1px solid #DEE2E6;
  padding: 5px 15px;
  cursor: pointer;
  font-size: 18px;
}
.btn:hover {
  background: #e4e8ec;
}
.btn.active {
  background: blue;
  color: #fff;
}
.option {
  margin: 2rem 0;
  padding: 1rem;
}
.option label {
  margin: 0;
  width: 95%;
  margin-left: 1rem;
  display: inline-block;
  cursor: pointer;
  font-size: 18px;
}
.option input {
  cursor: pointer;
}
.top {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 2rem;
  padding-top: 1rem;
}
.btn-end {
  background: #fff;
  float: right;
  border: 1px solid #DEE2E6;
  padding: 5px 15px;
  cursor: pointer;
  border-radius: 5px;
  font-size: 18px;
}
.btn-end:hover {
  background: #e4e8ec;
}
.answers {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 1rem;
  padding: 1rem 2rem 0 2rem;
}
.passed.active {
  color: green;
}
.failed.active {
  color: red;
}
@media screen and (max-width: 400px) {
  .container {
    width: 350px;
    margin: 0 auto;
  }
  .content {
    width: 100%;
    margin: 0 auto;
  }
  .top {
    display: flex;
  }
  .btn-end {
    margin-right: -1.5rem;
  }
  .btn {
    margin: 0 0;
    display: inline-block;
    width: 3rem;
  }
  .question p {
    margin-left: 2rem;
  }
}
</style>
