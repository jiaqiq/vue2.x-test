<template>
  <div>
    <el-table
      :data="tableData"
      :span-method="objectSpanMethod"
      :header-cell-style="headerCellStyle"
      style="width: 100%"
    >
      <!-- <el-table-column> -->
      <el-table-column prop="pickClass" label></el-table-column>
      <el-table-column prop="Pn" label></el-table-column>
      <!-- </el-table-column> -->

      <el-table-column label="ICC Value" header-align="center">
        <el-table-column prop="a1" label="A1" header-align="center">
          <template slot-scope="scope">
            <el-checkbox
              v-if="scope.$index != 10"
              v-model="scope.row.a1"
            ></el-checkbox>
            <span v-if="scope.$index == 10">{{ scope.row.a1 }}</span>
          </template>
        </el-table-column>
        <el-table-column prop="a2" label="A2" header-align="center">
          <template slot-scope="scope">
            <el-checkbox
              v-if="scope.$index != 10"
              v-model="scope.row.a2"
            ></el-checkbox>
            <span v-if="scope.$index == 10">{{ scope.row.a2 }}</span>
          </template>
        </el-table-column>
        <el-table-column prop="a3" label="A3" header-align="center">
          <template slot-scope="scope">
            <el-checkbox
              v-if="scope.$index != 10"
              v-model="scope.row.a3"
            ></el-checkbox>
            <span v-if="scope.$index == 10">{{ scope.row.a3 }}</span>
          </template>
        </el-table-column>
        <el-table-column prop="b1" label="B1" header-align="center">
          <template slot-scope="scope">
            <el-checkbox
              v-if="scope.$index != 10"
              v-model="scope.row.b1"
            ></el-checkbox>
            <span v-if="scope.$index == 10">{{ scope.row.b1 }}</span>
          </template>
        </el-table-column>
        <el-table-column prop="b2" label="B2" header-align="center">
          <template slot-scope="scope">
            <el-checkbox
              v-if="scope.$index != 10"
              v-model="scope.row.b2"
            ></el-checkbox>
            <span v-if="scope.$index == 10">{{ scope.row.b2 }}</span>
          </template>
        </el-table-column>
        <el-table-column prop="b3" label="B3" header-align="center">
          <template slot-scope="scope">
            <el-checkbox
              v-if="scope.$index != 10"
              v-model="scope.row.b3"
            ></el-checkbox>
            <span v-if="scope.$index == 10">{{ scope.row.b3 }}</span>
          </template>
        </el-table-column>
        <el-table-column prop="c1" label="C1" header-align="center">
          <template slot-scope="scope">
            <el-checkbox
              v-if="scope.$index != 10"
              v-model="scope.row.c1"
            ></el-checkbox>
            <span v-if="scope.$index == 10">{{ scope.row.c1 }}</span>
          </template>
        </el-table-column>
        <el-table-column prop="c2" label="C2" header-align="center">
          <template slot-scope="scope">
            <el-checkbox
              v-if="scope.$index != 10"
              v-model="scope.row.c2"
            ></el-checkbox>
            <span v-if="scope.$index == 10">{{ scope.row.c2 }}</span>
          </template>
        </el-table-column>
        <el-table-column prop="c3" label="C3" header-align="center">
          <template slot-scope="scope">
            <el-checkbox
              v-if="scope.$index != 10"
              v-model="scope.row.c3"
            ></el-checkbox>
            <span v-if="scope.$index == 10">{{ scope.row.c3 }}</span>
          </template>
        </el-table-column>
      </el-table-column>
      <el-table-column
        prop="sumOfPicks"
        label="Sum of Picks"
        header-align="center"
        width="120"
      ></el-table-column>
    </el-table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tableData: [{
        pickClass: 'Pick Class',
        Pn: 'P0 (N)',
        a1: false,
        a2: false,
        a3: false,
        b1: false,
        b2: false,
        b3: false,
        c1: false,
        c2: false,
        c3: false,
        sumOfPicks: '0'
      }, {
        pickClass: 'Pick Class',
        Pn: 'P1 (Z3)',
        a1: false,
        a2: false,
        a3: false,
        b1: false,
        b2: false,
        b3: false,
        c1: false,
        c2: false,
        c3: false,
        sumOfPicks: '553'
      }, {
        pickClass: 'Pick Class',
        Pn: 'P2 (Z2)',
        a1: false,
        a2: false,
        a3: false,
        b1: false,
        b2: false,
        b3: false,
        c1: false,
        c2: false,
        c3: false,
        sumOfPicks: '302'
      }, {
        pickClass: 'Pick Class',
        Pn: 'P3 (Z1)',
        a1: false,
        a2: false,
        a3: false,
        b1: false,
        b2: false,
        b3: false,
        c1: false,
        c2: false,
        c3: false,
        sumOfPicks: '210'
      }, {
        pickClass: 'Pick Class',
        Pn: 'P4 (Y3)',
        a1: false,
        a2: false,
        a3: false,
        b1: false,
        b2: false,
        b3: false,
        c1: false,
        c2: false,
        c3: false,
        sumOfPicks: '148'
      }, {
        pickClass: 'Pick Class',
        Pn: 'P5 (Y2)',
        a1: false,
        a2: false,
        a3: false,
        b1: false,
        b2: false,
        b3: false,
        c1: false,
        c2: false,
        c3: false,
        sumOfPicks: '120'
      }, {
        pickClass: 'Pick Class',
        Pn: 'P6 (Y1)',
        a1: false,
        a2: false,
        a3: false,
        b1: false,
        b2: false,
        b3: false,
        c1: false,
        c2: false,
        c3: false,
        sumOfPicks: '114'
      },{
        pickClass: 'Pick Class',
        Pn: 'P7 (X3)',
        a1: false,
        a2: false,
        a3: false,
        b1: false,
        b2: false,
        b3: false,
        c1: false,
        c2: false,
        c3: false,
        sumOfPicks: '170'
      },{
        pickClass: 'Pick Class',
        Pn: 'P8 (X2)',
        a1: false,
        a2: false,
        a3: false,
        b1: false,
        b2: false,
        b3: false,
        c1: false,
        c2: false,
        c3: false,
        sumOfPicks: '320'
      },{
        pickClass: 'Pick Class',
        Pn: 'P9 (X1)',
        a1: false,
        a2: false,
        a3: false,
        b1: false,
        b2: false,
        b3: false,
        c1: false,
        c2: false,
        c3: false,
        sumOfPicks: '364'
      },{
        sumOfPicksName: 'Sum of Picks',
        a1: 1,
        a2: 2,
        a3: 3,
        b1: 4,
        b2: 5,
        b3: 6,
        c1: 7,
        c2: 8,
        c3: 9,
        sumOfPicks: '2301'
      }]
    }
  },

   methods: {
    // 横向合并头部单元格
    headerCellStyle({ rowIndex, columnIndex }) {
      if(rowIndex === 0 && columnIndex === 0) {
        return {
          borderRight: 'none'
        }
      }
    },

    objectSpanMethod({ rowIndex, columnIndex }) {
      if(rowIndex != 10) {
        if (columnIndex === 0) {
          if (rowIndex === 0) {
            return {
              rowspan: 10,
              colspan: 1
            };
          } else {
            return {
              rowspan: 0,
              colspan: 0
            };
          }
        }
      }else {
        if(columnIndex === 0) {
          return [1, 2];
        }else if(columnIndex === 1) {
          return [0, 0];
        }
      }
    }
  }
}
</script>
