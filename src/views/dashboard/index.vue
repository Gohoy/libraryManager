<template>
  <div class="dashboard-container">
    <div title="Welcome" style="padding: 50px; overflow: hidden; color: #409eff;font: lighter 16px 'Lucida Sans Unicode';"
         data-options="iconCls:'icon-heart',plain:true">
        <b style="font-size: 36px; line-height: 30px; height: 30px;">Welcome to BookManager</b>
        <hr/>
        <b>develop environment</b>
        <p>JavaVersion: 1.8.0</p>
        <p>dataBase: MySQL 8.0</p>
        <p>forward: HTML+CSS+JavaScript+Vue+Axios+ElementUI</p>
        <p>backend: Java+SpringBoot+MyBatis+MySQL</p>
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  name: 'Dashboard',
  computed: {
    ...mapGetters([
      'id',
      'name',
      'roles'
    ])
  }
}
</script>
