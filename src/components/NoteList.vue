<template>
  <div class="note-list">
    <h2>Notes</h2>
    <ul>
      <li v-for="note in notes" :key="note.key">
        <p v-html="note.note"></p>
        <span>
            Posted by {{note.username}} @ {{ note.time }}
          </span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'NoteList',
  props : {
    notes : Array
  },
}
</script>