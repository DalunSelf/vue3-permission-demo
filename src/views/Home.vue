<template>
  <b-container>
    <div>

      <b-dropdown
        id="dropdown-1"
        text="選擇語系"
        class="m-md-2"
      >
        <b-dropdown-item
          v-for="localeObj in locales"
          :key="localeObj.locale"
          @click="$i18n.locale = localeObj.locale"
        >
          <span class="ml-50">{{ localeObj.name }}</span>
        </b-dropdown-item>
      </b-dropdown>

      <b-button
        variant="outline-primary"
        @click="$ability.update([{ action: 'manage', subject: 'all' }])"
      >
        {{ $t('admin') }}
      </b-button>

      <b-button
        variant="outline-primary"
        @click="$ability.update([{ action: 'read', subject: 'User' }])"
      >
        {{ $t('user') }}
      </b-button>

      <b-button
        variant="outline-primary"
        @click="$ability.update([{ action: 'read', subject: 'Member' }])"
      >
        {{ $t('editor') }}
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
  BDropdown, BDropdownItem,
  BCard, BCardText, BButton,
} from 'bootstrap-vue'
import { computed } from '@vue/composition-api'

export default {
  components: {
    BContainer,
    BRow,
    BCol,

    BDropdown,
    BDropdownItem,

    BCard,
    BCardText,
    BButton,
  },
  setup(_, { root }) {
    root.$ability.update([])

    const locales = [
      {
        locale: 'tw',
        name: '中文',
      },
      {
        locale: 'en',
        name: '英文',
      },
    ]

    const currentLocale = computed(() => locales.find(l => l.locale === root.$i18n.locale))

    return {
      locales,
      currentLocale,
    }
  },
}
</script>

<style>
</style>
