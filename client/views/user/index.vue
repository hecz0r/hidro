<template>
  <div>
    <div class="tile is-ancestor">
      <div class="tile is-parent is-vertical">
        <article class="is-child box">
          <p class="title">{{ user.displayName }}</p>
          <p class="subtitle">{{ user.email }}</p>
          <!-- <LinkedAccounts></LinkedAccounts> -->
        </article>
      </div>

      <!-- Main Column -->
      <div class="tile is-parent is-8 is-vertical">
        <article class="tile is-child box">
          <p class="title">Index</p>
          <Notes :completed="false"></Notes>
        </article>
        <article class="tile is-child box">
          <p class="title">Index trimis</p>
          <Notes :completed="true"></Notes>
        </article>
        <article class="tile is-child box">
          <p class="title">Trimite index</p>
          <NewNoteForm :preview="true"></NewNoteForm>
        </article>
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import LinkedAccounts from './LinkedAccounts'
import NewNoteForm from './NewNoteForm'
import Notes from './Notes'
export default {

  name: 'user',
  components: {
    NewNoteForm,
    Notes,
    LinkedAccounts
  },
  data () {
    return {
      title: 'Users'
    }
  },
  computed: {
    ...mapGetters({
      user: 'user',
      notes: 'notes'
    })
  },
  mounted () {
    this.$store.dispatch('initNotesRef')
  }
}
</script>

<style lang="scss" scoped>

</style>
