<script setup lang="ts">
import { ref } from "vue";
import Person from "./Person.vue";
import Subject from "./Subject.vue";
import AddEntity from "./AddEntity.vue";
import { random, shuffle } from "lodash-es";

const participant = ref("");
const participants = ref([
  "Jakub Fiejka",
  "Alexander Gvozdev",
  "Phillip  Barth",
  "Aleksey Korotkevich",
  "Łukasz Kępa",
  "Alex Bryniou",
  "Marcin Domański",
  "Piotr Jędrzejewski",
]);
const subject = ref("");
const subjects = ref(["Liked", "Learned", "Lacked", "Longed for"]);

const addParticipant = () => {
  if (participant.value === "") {
    return;
  }
  participants.value.push(participant.value);
  participant.value = "";
};
const removeParticipant = (index: number) => {
  participants.value.splice(index, 1);
};
const removeSubject = (index: number) => {
  subjects.value.splice(index, 1);
};
const addSubject = () => {
  if (subject.value === "") {
    return;
  }
  subjects.value.push(subject.value);
  subject.value = "";
};
const result = ref<{ name: string; people: string[] }[]>([]);
const randomize = () => {
  const temp = [...participants.value];
  const split = shuffle(
    subjects.value.map((s): { name: string; people: string[] } => ({
      name: s,
      people: [],
    }))
  );

  let splitCounter = 0;

  while (temp.length) {
    const el = temp.splice(random(temp.length - 1), 1)[0];
    split[splitCounter].people.push(el);
    splitCounter = splitCounter === split.length - 1 ? 0 : splitCounter + 1;
  }
  result.value = split;
};
</script>

<template>
  <div class="layout">
    <div class="participants">
      <h2 class="section-header">Participants</h2>
      <AddEntity v-model:value="participant" @add="addParticipant" />
      <ul>
        <li class="list-item" v-for="(participant, index) in participants">
          <Person
            :index="index"
            :person="participant"
            @remove="removeParticipant"
          />
        </li>
      </ul>
    </div>
    <div class="subjects">
      <h2 class="section-header">Subjects</h2>
      <AddEntity v-model:value="subject" @add="addSubject" />
      <ul>
        <li class="list-item" v-for="(subject, index) in subjects">
          <Subject :index="index" :subject="subject" @remove="removeSubject" />
        </li>
      </ul>
    </div>
    <div class="result">
      <button class="randomize-button" @click="randomize">Randomize</button>
      <div class="tiles">
        <div class="tile" v-for="item in result">
          <h2>{{ item.name }}</h2>
          <div>{{ item.people.join(", ") }}</div>
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped>
.layout {
  display: grid;
  grid-template-columns: 1fr 1fr 2fr;
  grid-template-rows: 1fr;
  gap: 2px 2px;
  grid-template-areas: ". . .";
  width: 100%;
  height: 100%;
  background-color: var(--darker-color);
}
.subjects {
  height: 100%;
  background-color: var(--dark-color);
}
.participants,
.subjects {
  padding: 4px;
}
.result {
  padding: 16px;
}
ul {
  padding: 0;
  margin: 0;
}
.list-item {
  padding: 0;
  margin: 0;
  list-style: none;
}
.section-header {
  padding: 0px 16px;
}
.tiles {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr 1fr;
  gap: 8px 8px;
  width: 100%;
  margin-top: 16px;
}
.tile {
  border-radius: 8px;
  min-height: 200px;
  padding: 24px;
  background: var(--dark-color);
}
.tile h2 {
  margin-top: 0;
}
.randomize-button {
  background: var(--primary-color);
  color: var(--text-color);
  padding: 8px 16px;
  outline: none;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
</style>
