<template>
  <div>
    <input type="text" v-model="board.content" v-on:keyup.enter="add">
    <button v-on:click="add">Save</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      board : {
        content : ''
      }
    }
  },

  methods: {
    add() {
      const content = this.board.content && this.board.content.trim();
      if (content == '') {
        alert('Please write the content');
        return;
      }

      this.$emit('dAdd', content);
      this.clearInput();
    },
    clearInput() {
      this.board.content = '';
    }
  }
}
</script>

<style scoped>
</style>
