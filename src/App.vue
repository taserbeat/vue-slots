<script setup lang="ts">
import { computed, DefineComponent, ref } from "vue";
import CardList from "./components/CardList.vue";
import SecondCardList from "./components/SecondCardList.vue";

type TabName = "first" | "second";

const selectedTabMame = ref<TabName>("first");

const updateTab = (tabName: TabName) => {
  selectedTabMame.value = tabName;
};

const selectedTab = computed(() => {
  switch (selectedTabMame.value) {
    case "first":
      return CardList;

    case "second":
      return SecondCardList;

    default:
      return CardList;
  }
});
</script>

<template>
  <div class="tab-changer">
    <button @click="updateTab('first')">Tab 1</button>
    <button @click="updateTab('second')">Tab 2</button>
  </div>
  <div class="tab-contents">
    <!-- <CardList></CardList> -->
    <component :is="selectedTab"></component>

    <!-- <CardList v-if="isFirstTab"></CardList>
    <SecondCardList v-if="!isFirstTab"></SecondCardList> -->
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.tab-contents {
  margin-top: 20px;
}
</style>
