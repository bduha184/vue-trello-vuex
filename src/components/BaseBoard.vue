<template>
  <div>
    <header>my Trello</header>
    <main>
      <p class="info-line">All: {{ totalCardCount }} tasks</p>
      <div class="list-index">
        <TaskList
          v-for="(item, index) in lists"
          :key="item.id"
          :title="item.title"
          :cards="item.cards"
          :listIndex="index"
          @change="movingCard"
        />
        <ListAdd />
      </div>
    </main>
  </div>
</template>

<script>
import ListAdd from "./ListAdd.vue";
import TaskList from "./TaskList.vue";
import { mapState } from "vuex";
export default {
  components: {
    ListAdd,
    TaskList,
  },
  methods:{
    movingCard(){
      this.$store.dispatch('updateList',{lists:this.lists})
    }
  },
  computed: {
    ...mapState(["lists"]),
    totalCardCount(){
      return this.$store.getters.totalCardCount
    }
  },
};
</script>
