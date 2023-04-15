<template>
  <div>
    <header>my Trello</header>
    <main>
      <p class="info-line">All: {{ totalCardCount }} tasks</p>
      <draggable class="list-index" :list="lists" @end="movingList">
        <TaskList
          v-for="(item, index) in lists"
          :key="item.id"
          :title="item.title"
          :cards="item.cards"
          :listIndex="index"
          @change="movingCard"
        />
        <ListAdd />
      </draggable>
    </main>
  </div>
</template>

<script>
import draggable from "vuedraggable";
import ListAdd from "./ListAdd.vue";
import TaskList from "./TaskList.vue";
import { mapState } from "vuex";
export default {
  components: {
    ListAdd,
    TaskList,
    draggable,
  },
  methods: {
    movingCard() {
      this.$store.dispatch("updateList", { lists: this.lists });
    },
    movingList(){
      this.$store.dispatch('upgradeList',{lists:this.lists})
    }
  },
  computed: {
    ...mapState(["lists"]),
    totalCardCount() {
      return this.$store.getters.totalCardCount;
    },
  },
};
</script>
