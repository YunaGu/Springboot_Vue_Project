<template>
  <div>
    <div style="padding-top: 20px">
      <el-button type="primary">Add</el-button>
      <el-button type="primary">Import</el-button>
      <el-button type="primary">Export</el-button>
    </div>
    <div style="padding: 20px 0">
      <el-input v-model="search" size="Medium" placeholder="Type to search" style="width: 20%"/>
      <el-button type="primary">search</el-button>
    </div>

    <el-table
        :data="tableData"
        :default-sort="{ prop: 'date', order: 'descending' }"
        style="width: 100%">
      <el-table-column prop="date" label="Date" sortable width="180" />
      <el-table-column prop="name" label="Name" width="180" />
      <el-table-column prop="address" label="Address" :formatter="formatter" />

      <el-table-column label="Operations">
        <template #default="scope">
          <el-button size="mini" @click="handleEdit(scope.$index, scope.row)"
          >Edit</el-button
          >
          <el-button
              size="mini"
              type="danger"
              @click="handleDelete(scope.$index, scope.row)"
          >Delete</el-button
          >
        </template>
      </el-table-column>

    </el-table>


    <div class="demo-pagination-block" style="padding-top: 20px">
      <el-pagination
          v-model:currentPage="currentPage4"
          :page-sizes="[5, 10, 15, 20]"
          :page-size="10"
          layout="total, sizes, prev, pager, next, jumper"
          :total="4"
          @size-change="handleSizeChange"
          @current-change="handleCurrentChange"
      >
      </el-pagination>
    </div>

  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: 'Home',
  components: {

  },
  data() {
    return {
      tableData: [
        {
          date: '2016-05-03',
          name: 'Tom',
          address: 'No. 189, Grove St, Los Angeles',
        },
        {
          date: '2016-05-02',
          name: 'John',
          address: 'No. 189, Grove St, Los Angeles',
        },
        {
          date: '2016-05-04',
          name: 'Morgan',
          address: 'No. 189, Grove St, Los Angeles',
        },
        {
          date: '2016-05-01',
          name: 'Jessy',
          address: 'No. 189, Grove St, Los Angeles',
        },
      ],
      search: '',
    }
  },
  methods: {
    handleEdit(index, row) {
      console.log(index, row)
    },
    handleDelete(index, row) {
      console.log(index, row)
    },
    currentPage4(){

    },
    handleSizeChange(){

    },
    handleCurrentChange(){

    },
    formatter(row, column) {
      return row.address
    },
  },
}
</script>
