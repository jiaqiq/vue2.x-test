<template>
  <div id="hello-world-container">
    <!-- <div>{{ arr }}</div> -->

    <div class="leftDiv"></div>
    <div class="centerDiv"></div>
    <div class="rightDiv"></div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      arr: [2, 1, 4, 5, 6, 9, 3, 7, 8],
    };
  },
  mounted() {
    this.arr = [...this.insertSort(this.arr)];
  },
  methods: {
    // 插入排序
    insertSort(arr) {
      for (var i = 1; i < arr.length; i++) {
        var curValue = arr[i];
        var j = i - 1;
        while (j >= 0 && curValue < arr[j]) {
          arr[j + 1] = arr[j];
          j--;
        }
        arr[j + 1] = curValue;
      }
      return arr;
    },
    //选择排序
    selectionSort(arr) {
      var minIndex, temp;
      for (var i = 0; i < arr.length - 1; i++) {
        minIndex = i;
        for (var j = i + 1; j < arr.length; j++) {
          if (arr[j] < arr[minIndex]) {
            minIndex = j;
          }
        }
        temp = arr[i];
        arr[i] = arr[minIndex];
        arr[minIndex] = temp;
      }
      return arr;
    },
    // 冒泡排序
    bubbleSort(arr) {
      for (var i = 0; i < arr.length; i++) {
        for (var j = 0; j < arr.length - 1 - i; j++) {
          if (arr[j] > arr[j + 1]) {
            var temp = arr[j + 1];
            arr[j + 1] = arr[j];
            arr[j] = temp;
          }
        }
      }
      return arr;
    },
  },
};
</script>


<style lang="scss">

  .leftDiv, .rightDiv {
    width: 200px;
    height: 200px;
    position: absolute;
    top: 0;
  }
  .leftDiv {
    background: red;
    left: 0;
  }
  .rightDiv {
    background: yellow;
    right: 0;
  }
  .centerDiv {
    background: pink;
    height: 200px;
  }
</style>
