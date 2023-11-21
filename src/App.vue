<template>
  <div id="app">
      <BoardAdd v-on:dAdd="add"></BoardAdd>
      <BoardList v-bind:dBoards="boards" v-on:dEdit="edit" v-on:dRemove="remove"></BoardList>
      <BoardFooter></BoardFooter>
  </div>
</template>

<script>
import BoardAdd from './components/BoardAdd.vue'
import BoardList from './components/BoardList.vue'
import BoardFooter from './components/BoardFooter.vue'

export default {
  data() {
    return {
      boards:  []
    }
  },
  created() {
    if (localStorage.length == 0) return;

    for (let i=0; i<localStorage.length; i++) {
      const key = localStorage.key(i);
      if (isNaN(key)) continue;

      let board = new Object();
      board.seq = key;
      board.content = localStorage.getItem(key);
      this.boards.push(board);
    }
  },
  methods: {
    add(content) {
      const idx = this.boards.length;
      const key = idx + 1;
      localStorage.setItem(key, content);

      let board = new Object();
      board.seq = key;
      board.content = content;
      this.boards.push(board);
    }
    ,edit(board, index) {
      localStorage.setItem(board.seq, board.content);
      this.boards.splice(index, 1, board);
    }
    ,remove(seq, index) {
      localStorage.removeItem(seq);
      this.boards.splice(index, 1);
    }
  },
  components: {
    'BoardAdd' : BoardAdd
    ,'BoardList' : BoardList
    ,'BoardFooter' : BoardFooter
  }
}
</script>

<style>
</style>
