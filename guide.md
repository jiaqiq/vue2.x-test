# 0. 指导书

# 1. 背景
该前端框架是一套基于Vue，[Element-ui](https://element.eleme.cn/#/zh-CN)进行二次开发封装的组件，兼容Element-ui的组件开发。是一套高度集成的前端组件。

框架提供了标准的增删改查页面模板，并集成了各类表单项内容（text，select等），简化了页面开发的复杂度，让开发人员更专注于自身的业务开发流程。

# 2. 版本组件信息

版本信息可以查看项目文件package.json, 以下列出一些主要的组件：

* 语言: JavaScript es6
* 框架： Vue，Vuex, Vue-roter, Vue-i18n
* 组件样式：Elment-ui
* mock工具：mockjs
* 表单验证：async-validator
* 异步调用：axios
* 打包工具: webpack

# 3. 运行环境及配置

### 3.1 如何运行guide book实例
步骤:
    - 启用guide book目录 （修改mock/index.js, 打开mockMenuTree() 来模拟菜单返回)
    - 使用dev环境启动项目， 即可访问菜单guide book，查看实例

### 3.2 启动命令：
使用npm启动的命令 可以在package.json scripts结点中查看.
SME开发运行环境：npm run dev:sme

### 3.3 配置
项目的配置目录：config/
配置包含了SMME和SME两个系统在SIT，UAT, PROD环境下的配置.


### 3.4 Router定义
vue router的定义在目录src/router下。
通过环境参数process.env.AREA 来区分SME和SMME系统的router导入。

# 4. 组件使用指导

### 4.1 页面排版
- src/pages/main/index.vue 定义了排版内容
- EwSide: src/components/layouts/side.vue 菜单侧边栏
- EwHead: src/components/layouts/head.vue 系统头部展示
- EwFoot: src/components/layouts/foot.vue 系统底部展示
- EwMain: src/components/layouts/main.vue 系统内容
- menuItem.vue: 菜单侧边栏视图
- tabsBtn.vue: 菜单标签视图

### 4.2 创建新的页面
- src/pages目录下创建vue文件
- 设置router (src/router)
- 定义初始化配置
- 编写页面控件内容

以下提供一个初始化的默认vue文件代码(参考src/pages/guideBook/template.vue) :
```
<!--

  SMIL Guide book
  Empty Template. You can copy it to create a new vue file.

  @author Dragon.Wang
-->
<template>
  <transition name="sys">
    <!-- component code -->
  </transition>
</template>

<!-- use ecmascript-6 -->
<script type="text/ecmascript-6">
  /* import base initialization method from mixins */
  /* a base smil page is made up of a search component, a table component, a dialog component */
  import {pageOptions, pageBtnClick, dialogOk} from "~/assets/js/mixins"

  //  /* import vue file like this, don't forget register the component in Components */
  //  import xxx from './xxxx.vue'
  //
  //  /* import util function from common, dict or other js file. */
  //  import { goSysAxios } from "~/assets/js/common";'

  export default {
    name: 'template', // name of the component
    components: {
      // define referenced component
    },

    props: {
      // define props of component
    },

    mixins: [
      // see pageOptions in mixins.js
      pageOptions(
        // searchOption data
        _this => [

        ],

        // mainTable buttons
        _this => [

        ],

        // table columns, without _this reference.
        [],

        // mainDialog data
        _this => [

        ],

        // callback, must be a function
        callback => {

        }
      ),

      // see pageBtnClick in mixins.js
      // define event for the buttons triggered by mainButtonClick method
      pageBtnClick(
        // disabledIndexs, index array of mainDialog data which you want to disable when 'update' button clicked.
        [],

        // multiSelectOptions, multi select event,
        [
          {
//            id: '', // button id, required.
//            message: '', // popup message, not required.
//            callback: (_this, selectValueId, selectValue) => {
//              // custom button event after you click ok button in popup. not required.
//            },
//            afterCallback: (_this, selectValue) => {
//              // callback of system button event when you do not define the callback method.
//            }
          }
        ],

        // addUpdateCallback, not required. callback after you click the button to display dialog.
        (_this, selectValue, id) => {

        },

        // otherButtonClick, not required. Custom button click event.
        (_this, id) => {

        }
      ),

      // To process the event of dialog
      dialogOk(
        // process before invoke the event.
        (resFormList, title, _this) => {

        },
        // add URL, not required, Object or String
        {
//          url: '',
//          type: ''
        },
        // update URL, not required, Object or String
        {

        },
        // Success callback, not required, Custom event after dialog ok.
        (data, _this) => {

        },

        // After callback, not required mutex with success callback.
        (formlist, title, _this, data) => {

        }
      )
    ],

    data() {
      return {
        // define variable of component
      }
    },

    watch: {
      // define variables to watch
    },

    methods: {
      // define methods of component
    },

    mounted() {
      // lifecycle of component
    }
  }
</script>

<!-- define scoped css style in this block. -->
<style lang="scss" scoped>
</style>

```

### 4.3 搜索框，表格，表单

#### 4.3.1 关于页面变量
SMIL框架中，通过引入Mixins中的pageOptions方法，进行页面的初始化, 定义了页面变量（可以参考本文 mixins.js），其中包括searchOption（搜索框对象）, mainTable（表格对象）, mainDialog（交互框对象）。页面上的主要事件和数据绑定都是通过这些对象进行的。

开发人员如果需要自定义的绑定模型，可以在data，computed等函数中进行定义。

#### 4.3.2 搜索框功能
搜索框是通过PageOptions中定义的searchOption对象进行遍历，展现相应的组件。
一个标准的搜索框实现代码：
```
<template v-if="searchShow">
    <ew-search
      name="partDemo"
      :option="searchOption.option"
      :formlist="searchOption.formlist"
      :ruleslist="searchOption.ruleslist"
      :noSetButton="true"
      @goSearch="goSearch"
      @goReset="goSearchReset"
    >
    </ew-search>
<template>
```
- option：定义搜索框的搜索页面内容
- formlist: 绑定模型
- ruleslist: async validator的rules，验证搜索框表单项
- noSetButton: 隐藏设置按钮
- goSearch: query按钮触发的emit事件
- goReset: reset按钮触发的emit事件

页面元素：
```
    - query按钮（触发goSearch事件）
    - reset按钮（触发goSearchReset事件）
    - 搜索输入框组件（由searchOption对象遍历生成）
```
@goSearch, @goSearchReset在mixins中有默认的实现：
```
goSearch() {
    this.searchTable(1)
},
//清空查询
goSearchReset() {
    this.searchTable(1)
},
```
点击query, reset按钮会触发当前页的table根据筛选条件检索数据并展现第一页数据。

搜索对象示例：
```
_this => [
  {
    type: 'text',
    name: 'lang.standardPage.partNo',
    field: 'partNo',
    required: false,
  },
  {
    type: 'text',
    name: 'lang.standardPage.partName',
    field: 'partName'
  },
],
```
- type：组件类型，实现是ew-condition，可以参考相关组件
- name：组件的placeholder展示，如果是多语言的key，则会显示对应的label, 否则显示字符串.
- field: 搜索时的参数名，后台分页时，会作为请求的参数，前台分页，则会根据筛选table中对应的属性。
- required: 是否必填（大多数情况下 不需要必填）。

#### 4.3.3 表格功能
SMIL表格是基于el-table二次封装的支持表内增删改查的组件。它提供了页面上做需的基本操作，使开发人员无需再关心如何放置页面上元素的问题，只需要进行简单的配置，就可以完成一个增删改查的页面。

一个标准ew-newtable的代码：
```
<div class="one-table">
    <ew-newtable
        editor
        name="partTable"
        ref="partTable"
        url="/parts"
        axiosType="get"
        :tableDataflag="tableDataflag"
        :requsetData="searchOption.formlist"
        :colums="mainTable.colums"
        :selected="mainTable.selected"
        :buttons="mainTable.buttons"
        :dialog="mainDialog"
        :dialogItems="mainDialog.option"
        @setSelected="(val) => this.mainTable.selected = val"
        @checkSelect="mainCheckSelect"
        @select="mainSelect"
        @buttonClick="(id, row) => mainButtonClick(id, row)"
    >
  </ew-newtable>
</div>
```
* div 的包层是必要的，不然button无法显示
* 支持ref定义，可以在页面中通过this.$refs控制table
* editor，控制table按钮事件的变量，为true时，button的onClick事件无效
* url, axiosType, requsetData（注意不是request, 框架拼写有问题）是table请求数据的参数，默认是分页请求
    如果不支持分页请求，可以通过datas，noPagination属性来传递数据
    如果支持前台分页请求，可以通过paginationType="front", datas属性来传递数据
* columns是pageOptions中定义的mainTable.columns对象，也可自定义。
* buttons是用来定义表上，和表行的动作按钮
* selected相关的，是当前选中项。
* buttonClick 是buttons触发的相关事件方法，mixins中有默认的实现方法mainButtonClick。
* dialog, dialogItems是按钮事件触发后的对象模型
* 支持slot定义
* 若不需要相应功能，可以查看newtable的参数, noSetBtn，noPagination, noAction等。

**columns的定义：**
```
[
  {
    prop: 'id',
    label: 'lang.standardPage.id',
    width: '180'
  },
  {
    prop: 'partNo',
    label: 'lang.standardPage.partNo',
    width: '180'
  },
  {
    prop: 'partName',
    label: 'lang.standardPage.partName',
    width: '180'
  },
  {
    prop: 'qty',
    label: 'lang.standardPage.qty',
    width: '180'
  },
  {
    prop: 'createTime',
    label: 'lang.standardPage.createTime',
    width: '180',
    dateFormatter: true,
  }
]
```
* prop: table数据结果集的属性
* label: i18n标签
* width: 列宽
* defined: 是否通过slot自定义列展示
* formatter/numberFormatter/dateFormatter: 列值的格式化，支持数字，日期等格式化
* yyyyMMdd: 日期格式转换成'yyyy-MM-dd'显示

详细的说明可以参考ew-newtable


**table button的定义:**
```
_this => [
  {
    id: 'add',
    name: 'lang.common.addItem',
    disabled: false,
    loading: false,
    icon: '',
    selectType: 'all'
  },
]
```
* id: Button的id
* name: Button的标签
* disabled: 是否可用
* loading: loading状态标识
* icon: Button的图标
* selectType: all(表格上方左侧排列), selectOne（行按钮）, right（表格上方右侧）

详细说明可以参考ew-button

**事件触发:**
***默认按钮事件触发：***
table组件定义了事件的触发函数，（若需要自定义按钮事件，通过onClick实现):
```
buttonClick(id, row, prop, it) {
    this.cellEditorProp = prop || 'all'
    if(id === 'update') {
      this.$emit('select', row) //点击行事件 row该行数据
    }
    if(this.editor) {
      this.editorClick(id, row)
    }
    if(it && it.onClick) {
      it.onClick(row)
    }
    else {
      this.$emit('buttonClick', id, row)
    }
  },
```
当按钮id是update时，会触发选中事件select
>@select="mainSelect"

mainSelect是mixins.js中定义的函数：
```
mainSelect(row) {
    this.mainTable.selected = row
},
```
当editor激活时，会执行newtable内置函数editorClick, 并且触发mainButtonClick函数，为弹出框进行赋值操作.

>@buttonClick="(id, row) => mainButtonClick(id, row)

mainButtonClick是定义在mixins.js的pageBtnClick函数中。

***行内编辑保存：***
ew-newtable组件定义了函数save(row)，来触发行内编辑保存的事件：可以通过一下函数进行控制。
editorSave: 自定义保存事件
beforeSave(formlist, data): 默认保存执行前的操作，可用来提示操作或者调用请求。formlist是表单对象，data是表格数据
save(row): 默认保存成功后的emit事件，row为当前保存成功的行。
如果是增加行，则默认的id是当前时间戳
如果是更新行，则默认保存删除是以id作为更新依据的。

***按钮是否显示可以通过button定义show函数来实现：***
```
show: (row) => {
  if(row.show) return true;
  return false;
}
```

***按钮自定义事件触发，通过onClick函数实现：***
```
{
    id: "downLoad",
    name: "lang.common.download",
    disabled: false,
    icon: "el-icon-download",
    selectType: "selectOne",
    onClick: (row) => {
      goSysAxios(url, params, type).then((result)=> {})
    },
}
```

### 4.3.4 表单选项
一个标准的表单实现
```
<div v-if="mainDiologVisible">
    <el-form
      :inline="true"
      label-width="200px"
      :model="mainDialog.formlist"
      class="form-inline line"
      :rules="mainDialog.ruleslist"
      ref="mainDialog"
    >
      <template v-for="(item,i) in mainDialog.option">
        <ew-condition :key="i" :option="item" :form="mainDialog.formlist" type="skip"></ew-condition>
      </template>
    </el-form>
</div>
```

表单模型一般与mainDialog进行绑定，页面的初始变量mainDiologVisible控制表单的显示与否。很多默认的实现中，都有直接改变mainDiologVisible变量值的操作，可以显示相应的表单项。

* inline: 一行显示（如果宽度允许）
* label-width: 表单的标签长度
* model: 表单模型，一般与mainDialog.formlist绑定，如果有冲突可以自定义变量绑定。
* rules: 表单校验规则
* ref：表单的句柄操作对象


### 4.4 通用JS文件.
#### mixins.js
Vue混入对象，pageOptions提供了页面的局部变量，例如mainTable, mainDialog等，pageBtnClick集成了button的默认操作mainButtonClick, 以及相关事件的触发操作（add, update, delete等）,dialogOk提供了默认的对话框确认事件。

##### pageOptions
mixin对象，混入data，mounted方法，初始化了vue页面的局部通用变量，定义了表格的按钮，列以及Dialog数据。
5个入参:
  - searchResData 搜索框数据定义
  - mainTableButtonsData 表格按钮定义
  - colums 表格列定义
  - dialogData 对话框数据定义
  - callback callback调用

data()变量定义：
- tableDataflag
    类型：String, 默认值为'0,0'
    格式：'0,0'，由逗号分隔的两个数字，第一个是timestamp，第二个是表格页数
    控制表格数据的变量，一般由search控件触发改变，通过newtable的数据绑定变量tableDataflag, 来达到刷新页面的目的。

- searchShow
    类型：布尔型，默认值为false
    用以控制search显示，当pageOptions的mounted函数流程执行完最后，会将该变量置位true, 通过v-if的方式，刷新显示搜索框。
    用法:
    ```
    <div class="paymentInformation">
        <template v-if="searchShow">
            <ew-search
                name="paymentInformation"
                ruleId="ruleForm"
                :option="searchOption.option"
                @goSearch="goSearch"
                @goReset="goSearchReset"
                :formlist="searchOption.formlist"
                :ruleslist="searchOption.ruleslist"
                :labelWidth="142"
                :noSetButton="true"
            />
        </template>
        ....
    </div>
    ```

- searchOption
    类型: 对象,
    搜索框的绑定对象, 可以通过直接操作该对象来获取搜索框的输入,以及改变搜索框的内容等.

    属性:
    - option
      搜索框组件的定义, 示例:
      ```
      <ew-search
        ...
        :option="searchOption.option"
        ...
      >
      </ew-search>

      ...

      {
        type: "text",
        name: "lang.customer.customerName",
        field: "name"
      }
      ```
    - formlist
      由定义的所有field属性组成的对象, 可以通过改对象直接改变搜索框的值.
      ```
       <ew-search
          ...
          :formlist="searchOption.formlist"
          ...
        >
        </ew-search>

        ...

        {
          ...
          // 日期控件选择日期后, 将date格式转换成带有时间(time)的日期格式
          onChange: val => {
              _this.searchOption.formlist.validEndTime = putDate(
                val + " 23:59:59"
              );
            },
        }
      ```

    - ruleslist
      搜索框的查询条件验证, 一般不是必要的, 可以通过定义属性required, 来设置必填的输入框.
      ```
      <ew-search
        ...
        :ruleslist="searchOption.ruleslist"
        ...
      >
      </ew-search>
      ...
      {
        type: "text",
        name: "lang.customer.customerName",
        field: "name"
        required: true,
      }
      ```
      校验的绑定是通过表单进行的, 可以参考async-validator, element-ui表单校验绑定以及search.vue
      ```
       // search.vue
       <el-form ...  :model="ruleForm" ... :rules="rules" :ref="ruleId">
       </el-form>
      ```

- mainTable
    类型: 对象
    表格的绑定对象, 定义了表格按钮, 列, 选中项等.

    - loading
    无实际使用情况,

    - buttons
    表格按钮的定义:
    ```
    <ew-newtable
       ...
        :buttons="mainTable.buttons"
        ...
    />

    {
      id: 'add',
      name: 'lang.common.addItem',
      disabled: false,
      selectType: 'all',
    }
    ```

    - columns
    表格列的定义:
    ```
    <ew-newtable
       ...
        :colums="mainTable.colums"
        ...
    />

    ...

    {
      prop: "code",
      label: "lang.customer.customerCode",
      width: "120"
    }
    ```

    - selected
    表格的选中列
    ```
    <ew-newtable
       ...
        :selected="mainTable.selected"
        @checkSelect="mainCheckSelect"
        @setSelected="val => (this.mainTable.selected = val)"
        ...
    />
    ...
    // 获取当前选中行
    this.mainTable.selected
    ```

    - checkSelecteds
    多选行项，当table的checkbox功能打开时，可以控制多选项，无须定义，table选中checkbox后，自动赋值.

    - defaultSearch
    默认为true， 控制table是否默认加载数据。

- mainDiologVisible
  主对话框是否可见的控制变量，集成于pageOption中，当触发mainButtonClick时，该变量置为true。
  内置closeMainDialog函数，置变量为false，来控制对话框关闭。
  ```
  // 控制dialog是否显示，关闭dialog对话框触发函数。
  <ew-dialog
        v-if="mainDiologVisible"
        ...
        @closeDialog="closeMainDialog"
      >
      ...
  </ew-dialog>

  ...

  // 也可以在页面中，直接修改该变量的值。
  closePrewDialog() {
      this.prew.diologVisible = false;
      this.mainDiologVisible = false;
  },

  ```

- mainDialog
对话框对象，定义了对话框按钮的状态，标题，控件，表单对象，规则。
属性：
    - loading
    按钮的loading状态，需要进行绑定。如果有多个loading状态控制，可以通过自定义loading变量绑定控制。
    ```
    // 控制对话框确定按钮的loading状态
    <ew-dialog
      ...
      :loading="mainDialog.loading"
      ...
    >
    </ew-dialog>

    // 操作dialog loading状态
    this.mainDialog.loading = true
    ```

    - title
    对话框的标题，add, update，preivew事件，均有自身的title赋值。另外，如果title是自定义的标题的话，也可以通过修改变量的值达到效果
    在对话框确认时，会根据title来判断执行add还是update的url操作。
    ```
    <ew-dialog
      ...
      :title="mainDialog.title"
      ...
    >
      ...
    </ew-dialog>
    ```

    - option
    对话框控件的定义，可以定义在table中，作为table事件触发的输入组件，也可以定义在form表单的显示里。
    需要控制控件的状态，可以通过操作该变量实现，改变控件的type会重新刷新控件
    ```
    // table控件的使用
    <ew-newtable
      ...
      :dialogItems="mainDialog.option"
      ...
    >
    </ew-newtable>

    // 对话框控件的布局
    <template v-for="(item,i) in mainDialog.option">
      <ew-condition :key="i" :option="item" :form="mainDialog.formlist" type="dialog"></ew-condition>
    </template>

    //弹出框数据
    _this => [
      {
        type: "text",
        name: "lang.partsExpenseVerification.detail.dcsExpenseVoucher",
        field: "expenseVoucherNo",
        disabled: true
      },
      ...
    ]

    // 改变控件位置，属性等。
    <script>
      ...
      let obj = this.mainDialog.option[2]
      this.mainDialog.option[0] = obj
      this.mainDialog.option.splice(2, 1)
      this.mainDialog.option[3].labelWidth = void 0
    </script>
    ```

    - formlist
    对话框的绑定对象，获取对话框控件的输入，也可以直接为对话框控件赋值。
    ```
    <ew-dialog
      ...
    >
      <el-form
        ...
        :model="mainDialog.formlist"
        ...
      >
        <template v-for="(item,i) in mainDialog.option">
          <ew-condition
            :key="i"
            :option="item"
            :form="mainDialog.formlist"
            type="skip"
            totalWidth="100%"
          ></ew-condition>
        </template>
      </el-form>
    </ew-dialog>
    ```

    - ruleslist
    对象类型，对话框控件的校验条件
    ```
    <ew-dialog
      ...
    >
      <el-form
        ...
        :rules="mainDialog.ruleslist"
        ...
      >
        ...
      </el-form>
    </ew-dialog>
    ```

- mounted() 函数
  mounted混入，负责vue的生命周期mounted中 加载搜索框，对话框组件，绑定对象，设置校验条件等操作。

##### pageBtnClick
定义页面button事件，共有4个入参，一个方法定义。
参数列表：
  - disabledIndexs
    数组类型，当button触发事件mainButtonClick, id为update时，必填，禁用定义在mainDialog中对应index的控件。

  - multiSelectOptions
    数组类型，定义按钮事件的弹框和请求等相关内容

  - addUpdateCallback
    函数，入参是(this, selectValue, id), selectValue是当前选中的行项，id为触发事件button的id
    弹出框事件赋值完成后的callback事件，可以额外处理自定义功能

  - otherButtonClick
    如果定义了该事件，则会在mainButtonClick最后进行调用，接受入参(this, id)

  实例说明:
  ```
  pageBtnClick(
      //当事件为update时，禁用dialog的第0，1，2个控件
      [0,1,2],
      //
      [
        {
          name: "dele", // id与button id一致，触发事件，当id为delete时，如果没有callback则，默认调用url的type为delete
          // message: "custom message", // 自定义弹框消息
          url: "dcs-sme-api/leadTime/", // url调用
          data: row => {  // url的参数，无定义，则默认是selectValue的id
            return row.lineNo;
          },
          callback: (_this, id, selectValue) => {
            // 如果url事件的type不是delete, 或者点击button弹框确认后需要自己处理事件，可以使用callback函数
          }
        }
      ],
      (_this, selectValue, id) => {
        // 处理addUpdateCallback
        _this.forSum();
      }
    ),
  ```

- dialogOk
  对话框确认事件，5个入参，可以添加事件的url以及callback
  参数列表：
    - res
    函数，必填。返回请求参数体，入参为(formlist, title, _this)，在点击对话框确认后，组装参数的函数。

    - addUrlRes
    String, add item时的请求url

    - changeUrlRes
    String, update item时的请求url

    - onSuccessCallback
    函数，请求成功后的callback，入参(data, _this) data为请求后的返回结果。不会弹出成功的消息，需要自己处理。

    - afterCallback
    函数，请求成功后，会根据事件，弹出成功的消息，如果存在aftercallbcak,则调用函数，入参是(formlist, title, _this, data)

#### dict.js
字典缓存对象，提供后台系统字典一次加载，多次使用。采用Promise对象，异步加载系统字典集。
使用场景： 前端有一些状态表示的参数，通常是以1，2等数字或者其他标识符传递的，后台不做转义（减少后台请求次数，和网络请求体的大小），那么我们需要重新获取字典表，进行映射。由于每次进入页面都会进行这样的请求，但请求在系统生命周期内变化的概率不大，因此，我们在系统第一次调用字典的时候，缓存获取到的字典表，这样可以减少字典表的网络请求。
使用方法如下：
  ```
  // 引入dict.js的字典方法
  import {getSalesOrderStatus, getSalesOrderType} from "~/assets/js/dict"
  ...

  // 使用字典方法获取字典数据，该方法只会加载一次字典集
  getSalesOrderStatus((dict) => {
      data.list.forEach(item => {
        let dictStatus = dict.find(dic => dic.dicKey == (item.dataStatus + ''))
        item.dataStatusName = dictStatus ? dictStatus.dicValue : ''
      })
    })

  ```

#### common.js
通用的JS方法，提供系统的异步调用，时间格式化等一系列的工具类方法, 以下介绍两个重要的方法，其余的可以自行查看源代码：
- goSysAxios(url, data={}, type, noErrorMeg)
  异步加载方法，SMIL框架的标准调用，table的加载就是使用该方法
  - url
  请求的path URL，不包含domain, domain定义为变量
  `getServerUrl = process.env.API_HOST`

  - data
  请求参数体，在不同的请求type下，会有不同的表现方式:
  type == 'get' 或者 'delete':
    - 参数为number，string类型或者对象只有一个属性时，会直接加载到url后面 e.g. goSysAxios('/test/', 123, 'get') => http://domain:port/test/123
    - 当url是mdm-api请求时，参数体有pageNo, pageSize并且参数个数等于3个，url中不包含query(这不是我写的条件。。): 会将第3参数直接放在url后，并在后面加上pageNo, pageSize
      e.g. goSysAxios('/test/', {a: '123', pageNo: 1, pageSize: 10}, 'get') => http://domain:port/test/123?pageNo=1&pageSize=10
    - 其余情况下，会把参数加在url后：
      e.g. goSysAxios('/test', {a: '123', b: '321'}, 'get') => http://domain:port/test?a=123&b=321

    type == 'post'或者'put': 参数会作为Request Body发送到服务器。
    在newtable中会有oneget和numPost，这个是因为分页参数不同的问题，dcs-sme-api的请求分页参数是pageNum, 详细可以参考newtable.vue文件。

  - type
  请求类型。只能接受'get', 'post', 'delete', 'put'

  **当后台返回的消息中，data.errorMsg属性不为空，并且noErrorMeg为false时，系统会自动使用MessageBox弹出错误信息。**

- downloadFile(url, date={}, method='get', _this, that, callback)
  下载excel的通用方法，参数有点啰嗦。
  - url
  下载请求的URL

  - date（参数名和意义不符，也不是我写的！）
  请求参数体（没有goSysAxios里的转换，直接作为Request Body）

  - method
  方法类型

  - _this
  当前页面对象，填写该参数后，会寻找_this.mainTable.button中name为lang.common.download的按钮（selectType=right)并置为loading状态。

  - that
  当前页面对象，填写该参数后，会将mainDialog.loading置为true, 这样下载的时候无法点击dialog的按钮。

  - callback
  完成下载后的callback方法。

#### filter.js
vue的过滤器方法，用以转义字典状态。

### 4.5 SMIL组件

#### eu-input-number
组件功能同el-input-number，数字输入框组件。
不同之处为：该组件小数点显示为逗号，同时，输入的时候可以输入逗号或者小数点作为小数点使用。
SME系统使用的数字控件为eu-input-number，SMME系统则为原来的el-input-number，（详情请参阅condition.vue中type === 'number'）

#### ew-condition
表单控件项，集成了多种控件形式，包括span, text, number, combo等等，控件在表单和表格中的行为一致，但是由于模型绑定的问题，在condition中使用了tableData来区分控件是否是在table中使用。
控件项的显示与否，使用了v-show="!option.hidden"， 这意味着在配置控件时，如果设置了hidden属性，则该控件不会出现在页面中。 常用的场景是页面表单中需要隐藏id的显示，使用hidden实现(属性只针对dialog的表达项，table列不生效)。
```
{
  type:"text",
  name:"id",
  field:"id",
  hidden:true
}
```
控件的通用属性和事件：
```
name:
  文本框的国际化label显示，表单项时，显示在文本框左侧，搜索项时，显示为placeholder, 表格编辑框时，不显示。

field:
  绑定变量名

clearBoth:
  清除浮动。

disabled:
  禁用状态。

required:
  是否是必填，用于表单校验。

width:
  可以用于控件的长度设置。

change, blur:
  事件触发函数，部分控件(date)的change事件函数是onchange, 有部分控件不具有blur事件，具体可参考代码。
```
各控件的常见使用方法：
- text
  常用于搜索框，表单，table编辑框，具有maxlength属性，可以控制输入框的最大输入长度。
  ```
  {
    type: "text",
    name: "lang.cstmEnquiry.dialog12",
    field: "incoterm",
  },
  ```

- span
  普通的div文本无框显示，支持numberFormatter和dateFormatter。
  ```
  {
    type: "span",
    name: "lang.paymentAdvice.table6",
    numberFormatter: 'price',
    field: "unpaidAmount"
  }
  ```
  当checkbox属性存在时，则转换成checkbox
  ```
  {
    type: "span",
    name: "lang.paymentAdvice.table114",
    numberFormatter: 'price',
    field: "advancedPayment",
    checkboxDisabled: false,
    checkbox: {
      default: true,
      change: (val) => {
        if(val) {
          _this.mainDialog.formlist.advancedPayment = _this.adviceRes
        }
        else {
          _this.mainDialog.formlist.advancedPayment = 0
        }
      }
    }
  },
  ```
- number
  数字控件，SME使用eu-input-number实现，SMME使用element-ui的el-input-number，区别在于小数点是否是使用逗号表示的。
  noControlBtn: 用来控制数字增减按钮的显示。
  max: 数字控件的最大值，默认是99999999999。
  min: 数字控件的最小值，默认是0。
  precision: 数字控件的精度，默认是0.
  afterText: 接受字符串，添加在数值后，常用在百分比显示数字。
  formatter: 格式化显示。
  接受change时间，无blur事件。
  ```
  {
    type: "number",
    name: "lang.advancedPayment.paymentAmount",
    field: "paymentAmount",
    required: true,
    max: 100,
    min: 0,
    precision: 2,
    afterText: '%',
    change: (val) => {
    },
    formatter: (val) => {
      return val * 100
    }
  },
  ```

- 组合框 combo, otherCombo, autoCombo
  组合框，可都选，可自定义选择的内容。autoCombo只有在SMME/partTracking中使用，是属于特例，只在特定的场景下有意义。
  combo, otherCombo功能类似，前者是适用于字典集组合框，后者增加了request参数，可以适用于一般的任何请求。实战中，我们更倾向于使用otherCombo，它可以适应几乎所有的场景使用，所以建议开发人员也使用otherCombo。
  multiple: 组合框多选，同element-ui功能
  remote & remote-method： 是否为远程搜索，同element-ui功能，实战中使用较少。
  twoText: 双文本显示，可参考purchasePriceMaintenance
  eu: 是否显示eu标识，当前国家选择是欧盟则显示欧盟图标。可参考customerManagement.vue
  ```
  {
    type: "otherCombo",
    name: "lang.purchasePrice.partName",
    field: "productNo",
    url: "dcs-sme-api/partData/match",
    comboValue: "productNo",
    comboText: "mdseName",
    twoText: true,
    filterable: true,
    searchName: "partOrName",
    requestItems: ["brandNo"],
    required: true
  },
  ```

- 时间 date，dataType
  时间控件，可以选择年月日, 多用于搜索框中。 dataType控件可以通过dateType指定类型：month, yyyyMM, yyyy
  limit: 过滤可以选择的日期。
  ```
  {
    type: "date",
    name: "lang.salesOrderApprove.search.submittedFrom",
    field: "submittedFrom",
    limit: time => {
      return new Date(_this.searchOption.formlist.submittedEnd) < time;
    },
    onChange: val => {
      _this.searchOption.formlist.submittedFrom = putDate(
        val + " 00:00:00"
      );
    }
  },

  // 输入年份的控件：
  {
    type: "datatype",
    dateType: "year",
    name: "lang.purchaseOrderApprove.table14",
    field: "sapAccYear",
    required: true
  },
  ```

- checkbox
  复选框，较少使用。可以参考element-ui的el-checkbox-group

- switch
  滑块控件。

- area
  多行文本

- address
  地址输入，使用el-cascader

- 上传组件 pic
  上传附件时使用的控件，控件上传成功后，会将附件的网络地址区分为domain:port/contextpath以及name 分别赋值给urlField和field属性。
  onlyPic：是否只能上传图片类型。
  ```
  {
    type: "pic",
    name: "lang.paymentAdvice.dialog6",
    field: "discrepancyAttName",
    urlField: "discrepancyAttUrl",
    url: "zuul/dcs-sme-api/inboundDiscrepancy/upload",
    onlyPic: false,
    required: true
  },
  ```

- radioGroup
  单选框组， deliverStatus.vue和customDeclarationNotice.vue中使用， SME新添加控件。

#### ew-dialog
Dialog对话框，有slot功能，可以在dialog中添加任意组件，一般用以弹出一条数据的明细信息，或者操作一些简单的功能。
弹出框也提供了滚动条的功能(isScroll)，预置了save按钮和其触发事件（也可自定义按钮和事件）。
以下是常规用法的示例：
```
<ew-dialog
    isScroll
    v-if="mainDiologVisible"
    :loading="mainDialog.loading"
    :title="mainDialog.title"
    :visible="true"
    :onlyPreview="false"
    @closeDialog="closeMainDialog"
    @ok="ok()"
    width="1000px">

    // 定义dialog里的组件内容
    ...

</ew-dialog>
```
用法解析：
Dialog对话框一般是由主页的表格数据操作（点击弹出明细，或者增加编辑按钮等）触发，因此在控制dialog是否显示的是否会使用mainDiologVisible这个mixins定义的页面变量（mixins的预置方法mainButtonClick会改变值，达到显示dialog的目的）。
loading则是表示Dialog对话框默认预置save按钮的loading状态，赋值后，点击按钮会将按钮状态变为loading。
title会影响到save按钮的显示，如果title是'lang.common.preview'（mainButtonClick, prev的情况下会将dialog title修改成该值），则save按钮不会显示，同样，如果将onlyPreview赋值为true, 则按钮不会显示（同时也包括自定义的按钮）。
closeDialog和ok是dialog窗口的触发事件，closeDialog是点击cancel后发生的事件，closeMainDialog是mixins内置事件，会将mainDiologVisible修改成false。
width用以控制dialog对话框的宽度。

如果需要自定义按钮和事件的话，可以参考：
```
<ew-dialog
  ...
  :okBtnOption="okBtnOption" // 用以修改ok button文字显示和图标
  :otherButtons="otherButtons" // 重新定义button组，与okBtnOption冲突.
  :otherButtonsClick="otherButtonsClick" // 重定义按钮组的事件
>
</ew-dialog>

data () {
  return {
    ...
    okBtnOption: {
      id: 'upload',
      name: 'lang.common.upload',
      icon: 'el-icon-upload2'
    },

    otherButtons: [
      {
        id: 'save',
        name: 'lang.common.submit',
        disabled: false,
        icon: 'el-icon-check'
      },
      {
        id: 'reject',
        name: 'lang.common.cancel',
        type: 'danger',
        disabled: false,
        icon: 'icon-zhongzhi'
      }
    ],
  }
},

method() {
  otherButtonsClick(id) {
    // 处理事件
    ...
  }
}

```

#### ew-newtable
table这一块，用法变化比较多，建议是参考newtable.vue的文件，来看实际的用法。
在此就简单介绍几种应用场景和它的实例文件：
  - 分页方式
    - 后台分页
    绝大部分的table是使用后台分页的，通过前台的pageNum(pageNo)以及pageSize来请求数据，这类页面都是包含url, axiosType, requsetData参数:
    ```
    <div class="one-table">
      <ew-newtable
        ...
        url="/url/test"
        axiosType="get"
        :requsetData="params"
      >
        ...
      </ew-newtable>
    </div>
    ```
    这类分页，通过参数请求数据，获得的结果是带分页信息的。
    可以参考purchaseOrderCreation.vue等许多页面查看具体用法。

    - 无分页
    有一类数据是不需要进行分页的，这时，table是不需要以上提及的后台分页参数的，只需要为datas进行赋值即可。
    ```
    <div class="one-table">
      <ew-newtable
        ...
        :datas="pageDatas"
      >
        ...
      </ew-newtable>
    </div>
    ```
    可以参考paymentConfirmDetail.vue， salesPriceHistoryPreivew等页面的table

    - 前台分页（SME新增功能）
    SME新需求，一般应用于part的显示，前台一次性获取所有数据，在前端完成分页和检索过滤的功能，可以有效的降低访问服务器的次数。
    这类表格，无配置后台分页的参数（url, axiosType），但是需要通过后台数据（一般使用goSysAxios方法）的加载并分配给table的datas属性，并将table的分页属性paginationType改为'front'（默认为backend)，requsetData会作为筛选项出现，要求筛选项的属性名必须和分页表格的属性名对应一致才能完成过滤的功能。
    ```
    <div class="one-table">
      <ew-newtable
        ...
        paginationType="front"
        :datas="importData"
      >
        ...
      </ew-newtable>
    </div>

    <script type="text/ecmascript-6">
      ...
      data() {
        return {
          ...
          importData: [],
          ...
        }
      },
      ...
      method() {
          mounted() {
            // 设置表格数据，也可以使用Axios完成网络请求
            this.importData = [1,2,3,4,5]
          }
      }

      ...
    </script>
    ```
    典型的案例有Customer的purchaseOrderCreationDetial.vue, salesOrderApproverDetail.vue等。

  - 表格数据格式化的问题
    我们在获取后台数据时，有些数据不是能直接显示给用户看的，例如状态，日期，价格等，都需要进行数据的格式化才能展示到table中。
    - 使用slot和filter
    newtable提供了slot, 可以让用户进行自定义的表格项编辑，包括添加超链接等操作，应用比较广泛。
    ```
    <div class="one-table">
      <ew-newtable
        ...
        ...
      >
        <span slot="purchaseOrderNo" class="link-style" slot-scope="scope" @click.stop="() => goDetail(scope.row)"
        >
          {{scope.value | filter}}
        </span>
      </ew-newtable>
    </div>
    ```

    - 使用tableDataFormat
    newtable同时也设置了tableDataFormat的方法，让用户对通过接口获取的数据进行格式化操作后，进行显示。
    ```
    <div class="one-table">
      <ew-newtable
        ...
        :tableDataFormat="tableDataFormat"
      >
        ...
      </ew-newtable>
    </div>

    <script>
      ...
      method() {
        tableDataFormat(data) {
          ...
          return data
        }
      }
    </script>
    ```

    - formatter
    newtable也内置了一些格式化的方法，dateFormatter, numberFormatter等，这些可以配置在列定义的时候。
    ```
    <script>
      mixins: [
        pageOptions(
          ...
          [
            {
              prop: "salesPrice",
              numberFormatter: 'numberForSme',
              label: "lang.salesDiscount.table8",
              width: "180"
            },

            {
              prop: "lastGrDate",
              label: "lang.partTracking.lastGRDate",
              width: 150,
              dateFormatter: true,
              yyyyMMdd: "yyyyMMdd"
            },
            ...
          ]
          ...
        )
      ]
      ...
    </script>
    ```

#### ew-search
主要属性：
```
formlist:
    搜索表单对象，可以直接获取搜索框中的数据, PageOptions进行初始化
name:
    搜索框名称
option:
    搜索组件定义项, PageOptions进行初始化
otherButtons:
    增加其他的按钮, option中定义onClick事件接受按钮点击事件
ruleslist:
    搜索框表单规则
noSetButton:
    不显示设置按钮
```
---
事件：
```
@goSearch:
    点击搜索时触发事件
@goReset:
    点击重置时触发事件
```

### 4.6 关于页面报错
#### Axios调用后台接口
后台接口的通用返回格式：
```
{
   success: true,
   data: {
   },
   errorCode: null,
   errorMsg: null,
}
```
当errorMsg不为空时，会通过alert框，弹出后台返回的errorMsg

#### 使用message或alert提示消息或者错误
```
this.$message({
    type: 'success', // error
    message: this.$t('lang.common.success'),
});

this.$alert(this.$t('lang.asnPost.errReceivedQtyBiggerThanAsnQty'), 'Warning', {
    type: 'error',
    confirmButtonText: 'Close'
})
```

### 4.7 关于角色权限相关
用户在登录SMIL系统后，系统会将权限存放在localStorage的roleCodeList变量中
v-smil-role指令可以用来控制控件的权限（参考directives/auth.js文件）：
```
// excluded：当权限为MENU_SMME_READONLY时，按钮不可见
<el-button
    v-smil-role="{excluded: ['MENU_SMME_READONLY']}"
    v-if = this.isCanceled
    style="margin-left: 10px"
    type="danger"
    @click="cancelHandle"
    >{{ $t("lang.common.cancel") }}</el-button
>
```

另外在vuex store中，我们也定义了相关的getter方法来判断权限，以供系统中必要的地方使用：
TODO: 此处可以优化一个通用的方法，和v-smil-role指令共用。
```
// 判断用户是否是dhl用户
if (this.$store.getters.isDhlUser) {
  this.cancelBtnActive = false
  this.nonPackedBtnActive = false
}
```

### 5. 编码规范及最佳实践
1. 代码命名使用驼峰规则
2. 组件之间的通信，使用props和emit
3. 后台传百分比数字，前台number控件显示时，可以添加afterText: '%'来显示百分比。
```
{
  type: "number",
  name: "lang.HSCode.importDuty",
  field: "importDuty",
  afterText: "%",
  precision: 2,
  min: 0,
  max: 100,
  required: true,
  formatter: val => {
    return val * 100;
  }
}
```
4. 表单校验
当未使用系统定义的功能时，表单若需校验，需要使用：this.$refs['mainDialog'].validate方法进行表单校验。 ref需要定义在el-form的ref参数中
```
<el-form
  ...
  ref="mainDialog"
>
</el-form>
```
