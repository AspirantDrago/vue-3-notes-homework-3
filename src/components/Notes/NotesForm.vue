<template>
  <div class="note-form__wrapper">
    <form class="note-form" @submit.prevent="onSubmit">
      <textarea
        required
        v-model="value"
        placeholder="Type our note"
      />
      <TagsList @onItemClick="handleTagClick" :items="tags" />
      <button class="btn btnPrimary" type="submit">submit</button>
    </form>
  </div>
</template>

<script>
import TagsList from '@/components/UI/TagsList';

export default {
  components: {
    TagsList,
  },
  data () {
    return {
      value: '',
      tags: [
        {
          title: 'home',
          isActive: false,
        },
        {
          title: 'work',
          isActive: false,
        },
        {
          title: 'travel',
          isActive: false,
        },
      ],
    };
  },
  methods: {
    resetForm () {
      this.value = '';
      this.tags.forEach(value => value.isActive = false);
    },
    onSubmit () {
      const note = {
        title: this.value,
        tags: this.tags.filter(value => value.isActive)
      }
      this.$emit('onSubmit', note);
      this.resetForm();
    },
    handleTagClick (tag) {
      tag.isActive = !tag.isActive;
    },
  },
}
</script>

<style lang="scss" scoped>
.note-form__wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.note-form {
  display: flex;
  flex-direction: column;
  max-width: 600px;
  width: 100%;

  textarea {
    margin-bottom: 0;
  }
}
</style>
