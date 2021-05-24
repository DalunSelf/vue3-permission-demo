<template>
  <b-container>
    <div>
      <b-button
        variant="outline-primary"
        @click="$ability.update([{ action: 'manage', subject: 'all' }])"
      >
        切換管理員
      </b-button>

      <b-button
        variant="outline-primary"
        @click="$ability.update([{ action: 'read', subject: 'User' }])"
      >
        切換使用者
      </b-button>

      <b-button
        variant="outline-primary"
        @click="$ability.update([{ action: 'read', subject: 'Member' }])"
      >
        切換小編
      </b-button>
    </div>

    <b-row>
      <b-col>
        <b-card
          v-if="$can('read', 'Admin')"
          title="Admin"
        >
          <b-card-text>此卡僅對“管理員”可見</b-card-text>
        </b-card>
      </b-col>

      <b-col>
        <b-card
          v-if="$can('read', 'User')"
          title="User"
        >
          <b-card-text>此卡僅對“使用者”可見</b-card-text>
        </b-card>
      </b-col>

      <b-col>
        <b-card
          v-if="$can('read', 'Member')"
          title="Member"
        >
          <b-card-text>此卡僅對“小編”可見</b-card-text>
        </b-card>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
import {
  BContainer, BRow, BCol,
  BCard, BCardText, BButton,
} from 'bootstrap-vue'

export default {
  components: {
    BContainer,
    BRow,
    BCol,

    BCard,
    BCardText,
    BButton,
  },
  setup(_, { root }) {
    root.$ability.update([])
  },
}
</script>

<style>
</style>
