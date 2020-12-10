<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <el-button type="primary" @click="dialogShow">打开弹框</el-button>

    <el-dialog title="样例弹框" :visible.sync="dialogVisible" width="600px">
     
      <div :style="`max-height:316px;overflow:auto;`">
         <el-table :data="gridDataComp" height="300">
            <el-table-column property="date" label="日期" width="150"></el-table-column>
            <el-table-column property="name" label="姓名" width="200"></el-table-column>
            <el-table-column property="address" label="地址"></el-table-column>
          </el-table>
      </div>
      <el-pagination
          background
          @current-change="handleCurrentChange"
          :current-page.sync="pageInfo.pageNo"
          :page-size.sync="pageInfo.pageSize"
          :page-sizes="[10, 20, 50, 100, 200]"
          layout="prev, pager, next"
          :total="gridData.length">
      </el-pagination>
      <span slot="footer" class="dialog-footer">
        <el-button @click="dialogCancel">关 闭</el-button>
        <el-button type="primary" @click="dialogCancel">确 定</el-button>
      </span>
    </el-dialog>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      pageInfo: {
        pageNo: 1,
        pageSize: 30,
        total: 0
      },
      gridData: [{
          date: '2016-05-02',
          name: '王小虎111',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '2016-05-04',
          name: '王小虎222',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '2016-05-01',
          name: '王小虎333',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '2016-05-03',
          name: '王小虎444',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '555',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎666',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎777',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎888',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎999',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎20',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎21',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎123',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎213',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎123',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎11',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎23',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎23',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎23',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎23',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎23',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎123',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎34',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎23',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎34',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎232',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎23',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎34',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎12',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎34',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎12',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎23',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎123',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎23',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎123',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-1205-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎123',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎123',
          address: '上海市普陀区金沙江路 1518 弄'
        },{
          date: '2016-05-01',
          name: '王小虎123',
          address: '上海市普陀区金沙江路 1518 弄'
        }],
        dialogVisible: false,
    }
  },
  computed: {
    gridDataComp() {
      return this.gridData.slice((this.pageInfo.pageNo-1)*this.pageInfo.pageSize,this.pageInfo.pageNo*this.pageInfo.pageSize)
    }
  },
  methods: {
    dialogShow() {
      this.dialogVisible = true;
    },
    dialogCancel() {
      this.dialogVisible = false;
    },
    handleCurrentChange(val) {
      console.log(val)
      this.pageInfo.pageNo = val;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

   /*修改滚动条样式*/
  .content-class::-webkit-scrollbar {
      width:10px;
      height:10px;
    }
  .content-class::-webkit-scrollbar-track {
      background: rgb(239, 239, 239);
      border-radius:2px;
    }
  .content-class::-webkit-scrollbar-thumb {
      background: rgba(0,0,0,0.10);
      border-radius:10px;
    }
  .content-class::-webkit-scrollbar-thumb:hover {
      background: rgba(0,0,0,0.25);
  }
</style>
