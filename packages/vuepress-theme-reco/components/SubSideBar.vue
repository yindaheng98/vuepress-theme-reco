<template>
  <ul class="sub-sidebar-wrapper">
    <li
      v-for="(header, index) in $page.headers"
      :key="index"
      :class="[`level-${header.level}`, isActive(header)? 'active': '']"
    >{{ header.title }}</li>
  </ul>
</template>

<script>
import { isActive } from '@theme/helpers/utils'

export default {
  computed: {
    headers () {
      const headers = this.$page.headers.filter(header => header.level === 2)
      return headers
    }
  },
  methods: {
    isActive (header) {
      return isActive(this.$route, this.$page.path + '#' + header.slug)
    }
  }
}

</script>

<style lang="stylus" scoped>
.sub-sidebar-wrapper
  padding-left 0
  list-style none
  border-left 1px solid var(--border-color)
  font-size 12px
  li
    padding .5rem 0
    cursor pointer
    &:hover
      color $accentColor
    &.active
      border-left 1px solid $accentColor
      color $accentColor
    &.level-1
      padding-left .4rem
    &.level-2
      padding-left .9rem
    &.level-3
      padding-left 1.2rem
</style>

