<template>
  <div class="list" >
    <div class="listheader">
      <p class="list-title">{{ title }}</p>
      <p class="list-counter">total:{{ totalCardInList }}</p>
      <div class="deletelist" @click="removeList">×</div>
    </div>
    <draggable group="cards" :list="cards" @end="$emit('change')">
      <CardBody
        v-for="(item,index) in cards"
        :body="item.body"
        :key="item.id"
        :cardIndex="index"
        :listIndex="listIndex"
      />
      <CardAdd :listIndex="listIndex"/>
    </draggable>
  </div>
</template>

<script>
import CardAdd from './CardAdd.vue'
import CardBody from './CardBody.vue'
import draggable from 'vuedraggable'

export default {
  components:{
    CardAdd,
    CardBody,
    draggable,
  },
  props: {
    title: {
      type: String,
      required: true,
    },
    cards:{
      type:Array,
      required:true
    },
    listIndex: {
      type: Number,
      required: true,
    },
  },
  methods: {
    removeList: function () {
      if (confirm("本当にこのリストを削除しますか？")) {
        this.$store.dispatch("removelist", { listIndex: this.listIndex });
      }
    },
  },
  computed:{
    totalCardInList(){
      return this.cards.length;
    }
  }
};
</script>
