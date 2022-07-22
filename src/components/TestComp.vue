<template>
  <div class="questions">
      <div class="question"> <span>{{currentIndex+1}})</span> <p>{{element.question}}</p> </div>
      <div class="form-content" :class="{active: hasEnd}">
      <div class="option">    
        <input v-if="!hasEnd" type="radio" id="typeA" name="questions" v-model="answers[currentIndex]" :value="element.option[0].isTrueA">
        <label for="typeA" :class="{active : (element.option[0].isTrueA== true) && hasEnd}">{{element.option[0].typeA}}</label>
        <div class="custom-radio"></div>
      </div>
      <div class="option">
        <input v-if="!hasEnd" type="radio" id="typeB" name="questions" v-model="answers[currentIndex]" :value="element.option[1].isTrueB">
        <label for="typeB" :class="{active : (element.option[1].isTrueB== true) && hasEnd}">{{element.option[1].typeB}}</label>
        <div class="custom-radio"></div>
      </div>
      <div class="option">
        <input v-if="!hasEnd" type="radio" id="typeC" name="questions" v-model="answers[currentIndex]" :value="element.option[2].isTrueC">
        <label for="typeC" :class="{active : (element.option[2].isTrueC== true) && hasEnd}">{{element.option[2].typeC}}</label>
        <div class="custom-radio"></div>
      </div>
      </div>
    </div>
</template>

<script>
export default {
props: ["element", "currentIndex", "index", "hasEnd"],
data() {
  return {
    answers: [],
    currentOption: ""
  }
},
methods: {
  sumAnswers() {
    let answerSum = this.answers;
    return answerSum;
  }
},
mounted() {
  
}
}
</script>

<style>
.questions {
  background: #e8ebf1;
  padding: 2rem;
}
.form-content.active label {
  cursor: auto;
}
.option {
  position: relative;
}
label.active ~ .custom-radio::after {
  display: block;
}
.custom-radio::after {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  width: 1.5rem;
  content: "";
  font-size: 20px;
  background: rgb(40, 175, 58);
  display: none;
}
.custom-radio.active {
  color: red;
}
.typeA.active ~ label {
  color: red;
}
[type="radio"]:checked,
[type="radio"]:not(:checked) {
    position: absolute;
    left: -9999px;
}
[type="radio"]:checked + label,
[type="radio"]:not(:checked) + label
{
    position: relative;
    padding-left: 28px;
    cursor: pointer;
    line-height: 20px;
    display: inline-block;
    color: #666;
}
[type="radio"]:checked + label:before,
[type="radio"]:not(:checked) + label:before {
    content: '';
    position: absolute;
    left: 0;
    top: 0;
    width: 18px;
    height: 18px;
    border: 1px solid #ddd;
    border-radius: 100%;
    background: #fff;
}
[type="radio"]:checked + label:after,
[type="radio"]:not(:checked) + label:after {
    content: '';
    width: 12px;
    height: 12px;
    background: #F87DA9;
    position: absolute;
    top: 4px;
    left: 4px;
    border-radius: 100%;
    -webkit-transition: all 0.2s ease;
    transition: all 0.2s ease;
}
[type="radio"]:not(:checked) + label:after {
    opacity: 0;
    -webkit-transform: scale(0);
    transform: scale(0);
}
[type="radio"]:checked + label:after {
    opacity: 1;
    -webkit-transform: scale(1);
    transform: scale(1);
}

</style>