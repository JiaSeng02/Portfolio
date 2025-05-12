<template>
  <div class="app-container">
    <Layout>
      <template #left>
        <div class="aside">
          <SiteAside></SiteAside>
        </div>
      </template>
    </Layout>
  </div>
</template>

<script>
import Layout from '@/components/Layout/index.vue'
import SiteAside from '@/components/SiteAside/index.vue'

export default {
  components: {
    Layout,
    SiteAside,
  },
}
</script>

<style scoped></style>
