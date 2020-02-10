<template>
  <div class="flex">
    <div class="left-side">
      <h3 class="title">Content</h3>
      <draggable class="dragArea list-group" :list="list1" group="people" @change="log">
        <div class="list-group-item" v-for="element in list1" :key="element.id">
          <template v-if="element">
    
            <component v-bind:is="element.name"></component>
          </template>
        </div>
        <button slot="footer" @click="addPeople">Add</button>
      </draggable>
    </div>

    <div class="right-side">
      <h3 class="title">Sections</h3>
      <draggable
        class="dragArea list-group"
        :sort="false"
        :list="list2"
        :group="{ name: 'people', pull: 'clone', put: false }"
        @change="log"
      >
        <div class="list-group-item" v-for="element in list2" :key="element.name">{{ element.name }}</div>
      </draggable>
    </div>
  </div>
</template>
//https://coolors.co/993955-ae76a6-a3c3d9-ccd6eb-e9ecf5
<script>
import draggable from "vuedraggable";
import texte from "./text";
export default {
  name: "clone",
  display: "Clone",
  order: 2,
  components: {
    draggable,
    texte
  },
  data() {
    return {
      list1: [],
      list2: [
        { id: 1, name: "texte" },
        { id: 2, name: "Gallerie" },
        { id: 3, name: "Video" },
        { id: 4, name: "Quiz" }
      ]
    };
  },
  methods: {
    addPeople(e) {},
    log: function(evt) {
      window.console.log(evt);
    }
  }
};
</script>

<style scoped>
.flex {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
.left-side {
  text-align: left;
  padding: 20px;
  background: #CCD6EB;
  flex: 1 70%;
}
.right-side {
  padding: 20px;
  background: #E9ECF5;
}
.list-group-item {
  padding: 10px;
  background: #A3C3D9;
  margin: 2px auto;
}
.title {
  color: #993955;
}
.dragArea {
  background: #993955;
}
</style>