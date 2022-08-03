<template>
  <div class="note-add">
    <textarea type="text" class="form-control" v-model="note"></textarea>
    <br />
    <button v-on:click="addNote(note)" type="button">Save</button>
  </div>
</template>

<script>
export default {
  name: 'NoteAdd',
  props: {
    authUser : Object
  },
  data : function(){
    return {
      note: ''
    }
  },
  methods: {
    addNote: function(noteText){
      if (noteText.trim() === '') {
        return false;
      }

      //For this example, we'll just save notes to local storage.
      //in a real application, it will go to your database
      let notesJson = localStorage.getItem('notes');
      let notes = [];

      if (notesJson == null) {
        notes = [];
      } else {
        notes = JSON.parse(notesJson);
      }
      const note = {
        key : Math.random(),
        note : noteText,
        username : this.authUser.username,
        time : new Date().toDateString()
      };
      notes.unshift(note);
      localStorage.setItem('notes', JSON.stringify(notes));

      //Clear the note input once we've added it to local storage
      this.note = '';
      //Let the parent know we added a note
      this.$emit("noteAdded", note)
    }
  }
}
</script>