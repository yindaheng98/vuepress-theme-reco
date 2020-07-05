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
    isLinkActive (header) {
      return isActive(this.$route, this.$page.path + '#' + header.slug)
    }
  },
  render (h) {
    return h('ul', {
      class: { 'sub-sidebar-wrapper': true }
    }, [
      ...this.headers.map(header => {
        return h('li', {
          class: {
            active: this.isLinkActive(header),
            [`level-${header.level}`]: true
          },
          attr: { key: header.title }
        }, [
          h('router-link', {
            class: { 'sidebar-link': true },
            props: { to: `${this.$page.path}#${header.slug}` }
          }, header.title)
        ])
      })
    ])
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
    border-left 1px solid transparent
    a
      color var(--text-color)
    &:hover
      a
       color $accentColor
    &.active
      border-left 1px solid $accentColor
      a
       color $accentColor
    &.level-1
      padding-left .4rem
    &.level-2
      padding-left .9rem
    &.level-3
      padding-left 1.2rem
</style>

