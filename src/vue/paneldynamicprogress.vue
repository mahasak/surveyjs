<template>
    <div>
        <input type="range" v-if="question.isRangeShowing" min="0" :max="rangeMax" :value="question.currentIndex" style="width:25%;float:left;margin:5px" @change="changeRange" />
        <input type="button" v-if="question.isPrevButtonShowing" :value="question.panelPrevText" style="float:left;margin:5px"  :class="question.cssClasses.button"  @click="prevPanelClick" />
        <input type="button" v-if="question.isNextButtonShowing" :value="question.panelNextText"  style="float:left;margin:5px"  :class="question.cssClasses.button"  @click="nextPanelClick" />
        <input type="button" v-if="question.canAddPanel" :value="question.panelAddText" style="float:left;margin:5px"  :class="question.cssClasses.button"  @click="addPanelClick"/>
    </div>
</template>

<script lang="ts">
import Vue from "vue";
import { Component, Prop } from "vue-property-decorator";
import { default as Question } from "./question";
import { Question as QuestionModel } from "../question";
import { PanelModel } from "../panel";
import { QuestionPanelDynamicModel } from "../question_paneldynamic";

@Component
export default class PanelDynamicProgress extends Vue {
  @Prop question: QuestionPanelDynamicModel;

  get rangeMax() {
    return this.question.panelCount - 1;
  }
  addPanelClick() {
    this.question.addPanelUI();
  }
  prevPanelClick() {
    this.question.currentIndex--;
  }
  nextPanelClick() {
    this.question.currentIndex++;
  }

  changeRange(event) {
    this.question.currentIndex = event.target.value;
  }
}

Vue.component("survey-paneldynamicprogress", PanelDynamicProgress);
</script>
