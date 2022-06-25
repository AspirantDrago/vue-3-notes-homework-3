<template>
  <div>
    <NotesForm @onSubmit="handleSubmit" />
    <NotesList :items="notes" @onRemove="handleRemove" />
  </div>
</template>

<script>
import NotesForm from '@/components/Notes/NotesForm';
import NotesList from '@/components/Notes/NotesList';
import notes from '@/seeders/notes';

export default {
  components: {
    NotesForm,
    NotesList,
  },
  data () {
    return {
      notes: notes,
    };
  },
  mounted () {
    this.getNodes();
  },
  watch: {
    notes: {
      handler (updatedList) {
        localStorage.setItem('notes', JSON.stringify(updatedList));
      },
      deep: true,
    }
  },
  methods: {
    // * get / set notes
    getNodes () {
      const localNotes = localStorage.getItem('notes');
      if (localNotes) {
        this.notes = JSON.parse(localNotes);
      }
    },
    // * submit notes
    handleSubmit (note) {
      this.notes.push(note);
    },
    // * remove note
    handleRemove (index) {
      this.notes.splice(index, 1);
    }
  },
};
</script>
