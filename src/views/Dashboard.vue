<template>
  <div>
    <Header />
    <Table />   
  </div>
</template>

<script>
import Header from '@/components/Header.vue'
import Table from '../components/Table.vue'


export default {
    name: 'Dashboard',
    components: {
        Header,
        Table,
    }
}
</script>

<style scoped>

</style>