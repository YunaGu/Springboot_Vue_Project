<template>
  <div>
<!--    button    -->
    <div style="padding-top: 20px">
      <el-button type="primary" @click="add">Add</el-button>
      <el-button type="primary">Import</el-button>
      <el-button type="primary">Export</el-button>
    </div>

<!--    search    -->
    <div style="padding: 20px 0">
      <el-input v-model="search" size="Medium" placeholder="Type to search" style="width: 20%" clearable/>
      <el-button type="primary" @click="load">search</el-button>
    </div>

<!--table-->
    <el-table
        :data="tableData"
        :default-sort="{ prop: 'date', order: 'descending' }"
        style="width: 100%">
      <el-table-column prop="id" label="ID" sortable width="180" />
      <el-table-column prop="username" label="Username" width="180" />
      <el-table-column prop="age" label="Age" width="180" />
      <el-table-column prop="sex" label="Sex" width="180" />
      <el-table-column prop="address" label="Address" :formatter="formatter" />

      <el-table-column label="Operations">
        <template #default="scope">
          <el-button size="mini" @click="handleEdit(scope.row)">Edit</el-button>
          <el-button size="mini" type="danger" @click="handleDelete(scope.$index, scope.row)">Delete</el-button>
        </template>
      </el-table-column>

    </el-table>

<!--pages-->
    <div class="demo-pagination-block" style="padding-top: 20px">
      <el-pagination
          @size-change="handleSizeChange"
          @current-change="handleCurrentChange"
          :currentPage="currentPage"
          :page-sizes="[5, 10, 20]"
          :page-size="pageSize"
          layout="total, sizes, prev, pager, next, jumper"
          :total="total"
      >
      </el-pagination>
    </div>

<!--Dialog-->
    <el-dialog v-model="dialogVisible" title="ADD">
      <el-form :model="form">
        <el-form-item label="ID" :label-width="formLabelWidth">
          <el-input v-model="form.id" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="Username" :label-width="formLabelWidth">
          <el-input v-model="form.username" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="Age" :label-width="formLabelWidth">
          <el-input v-model="form.age" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="Sex" :label-width="formLabelWidth">
          <el-radio-group v-model="form.sex">
            <el-radio label="Male"></el-radio>
            <el-radio label="Female"></el-radio>
            <el-radio label="Unknown"></el-radio>
          </el-radio-group>
        </el-form-item>
        <el-form-item label="Address" :label-width="formLabelWidth">
          <el-input type="textarea" v-model="form.address" autocomplete="off"></el-input>
        </el-form-item>
      </el-form>
      <template #footer>
        <span class="dialog-footer">
          <el-button @click="dialogVisible = false">Cancel</el-button>
          <el-button type="primary" @click="save(); dialogVisible = false">Confirm</el-button>
        </span>
      </template>
    </el-dialog>

  </div>
</template>

<script>
// @ is an alias to /src

import request from "../utils/request";

export default {
  name: 'Home',
  components: {

  },
  data() {
    return {
      dialogVisible: false,
      form: {},
      formLabelWidth: '120px',
      search: '',
      currentPage: 1,
      pageSize: 10,
      total: 0,
      tableData: []
    }
  },
  created(){
    this.load()
  },
  methods: {

    load(){
      request.get("/api/user",{
        params:{
          pageNum: this.currentPage,
          pageSize: this.pageSize,
          search: this.search
        }
      }).then(res => {
        console.log(res)
        this.tableData = res.data.records;
        this.total = res.data.total;
      })
    },
    add(){
      this.dialogVisible = true;
      this.form = {}
    },
    save(){
      if (this.form.id){//update
        request.put("/api/user", this.form).then(res => {
          console.log(res)
          this.load()
        })
      }else {//add
        request.post("/api/user", this.form).then(res => {
          console.log(res)
          this.load()
        })
      }
    },
    handleEdit(row) {
      console.log(row)
      this.form = JSON.parse(JSON.stringify(row))
      this.dialogVisible = true
    },
    handleDelete(index, row) {
      console.log(index, row)
    },
    currentPage4(){

    },
    handleSizeChange(pageSize){
      this.pageSize = pageSize
      this.load()
    },
    handleCurrentChange(pageNum){
      this.currentPage = pageNum
      this.load()
    },
    formatter(row, column) {
      return row.address
    },
  },
}
</script>
