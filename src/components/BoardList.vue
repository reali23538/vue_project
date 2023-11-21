<template>
  <table>
    <tr>
      <th>seq</th>
      <th>content</th>
      <th>edit/remove</th>
    </tr>
    <tr v-for="(board, index) in dBoards" :key="board">
      <td>
        {{ board.seq }}
      </td>
      <td>
        <input type="text" v-model="board.content">
      </td>
      <td>
        <button v-on:click="edit(board, index)">Edit</button>
        <button v-on:click="remove(board.seq, index)">Delete</button>
      </td>
    </tr>
    <tr v-if="dBoards.length==0">
      <td colspan="3">no contents</td>
    </tr>
  </table>
</template>

<script>
export default {
  props: ['dBoards'],
  methods: {
    edit(board, index) {
      this.$emit('dEdit', board, index);
    }
    ,remove(seq, index) {
      this.$emit('dRemove', seq, index);
    }
  }
}
</script>

<style>
</style>
