<template>
  <div class="app-container">
    <Search :query="query"/>
    <!--表格渲染-->
    <el-table v-loading="loading" :data="data" size="small" style="width: 100%;">
      <el-table-column prop="nickname" label="用户名"/>
      <el-table-column prop="requestIp" label="IP"/>
      <el-table-column prop="address" label="地址来源"/>
      <el-table-column prop="description" label="描述"/>
      <el-table-column prop="createTime" label="创建日期" width="180px">
        <template slot-scope="scope">
          <span>{{ parseTime(scope.row.createTime) }}</span>
        </template>
      </el-table-column>
    </el-table>
    <!--分页组件-->
    <el-pagination
      :total="total"
      :current-page="page + 1"
      style="margin-top: 8px;"
      layout="total, prev, pager, next, sizes"
      @size-change="sizeChange"
      @current-change="pageChange"/>
  </div>
</template>

<script>
import initData from '@/mixins/crud'
import { parseTime } from '@/utils/index'
import Search from './search'
export default {
  name: 'Log',
  components: { Search },
  mixins: [initData],
  created() {
    this.$nextTick(() => {
      this.init()
    })
  },
  methods: {
    parseTime,
    beforeInit() {
      this.url = 'api/logs/mlogs'
      const sort = 'id,desc'
      const query = this.query
      const value = query.value
      this.params = { page: this.page, size: this.size }
      if (value) { this.params['blurry'] = value }
      return true
    }
  }
}
</script>

<style scoped>

</style>
