<template>
  <div style="margin: 20px;">
    <el-input
      v-model="input"
      placeholder="请输入内容"
      class="font-size-extra-large"
    ></el-input>
    <div style="margin: 20px;">
      <el-button type="primary" size="mini">新建项目</el-button>
      <el-button type="primary" size="small">新建文件夹</el-button>
      <el-button type="primary" size="medium">新建项目</el-button>
      <el-button type="primary">新建文件夹</el-button>
    </div>
    <div style="margin: 20px;">
      <el-button type="info">提交订单</el-button>
      <el-button type="primary">提交订单</el-button>
    </div>
    <div style="margin: 20px;">
      <el-button>取消</el-button>
      <el-button type="primary">查询</el-button>
    </div>
    <div style="margin: 20px;">
      <el-button>知道了</el-button>
      <el-button>不再提示</el-button>
    </div>
    <div style="margin: 20px;">
      <el-button type="primary">设置完毕</el-button>
    </div>
    <div style="margin: 20px;">
      <el-button>返回上一步</el-button>
      <el-button type="primary">设置完毕，下一步</el-button>
    </div>

    <div style="margin:20px">
      <el-input placeholder="输入充值金额" v-model="input2">
        <el-button slot="append" type="primary">确定</el-button>
      </el-input>
    </div>

    <div style="margin:20px">
      单选框
      <el-radio v-model="radio" label="1">未选中</el-radio>
      <el-radio v-model="radio" label="2">选中</el-radio>
      <el-radio disabled v-model="radio" label="1">禁用</el-radio>
      <el-radio disabled v-model="radio" label="2">选中且禁用</el-radio>
    </div>

    <div style="margin:20px">
      复选框
      <el-checkbox-group v-model="checkList">
        <el-checkbox label="复选框 A"></el-checkbox>
        <el-checkbox label="复选框 B"></el-checkbox>
        <el-checkbox label="复选框 C"></el-checkbox>
        <el-checkbox label="禁用" disabled></el-checkbox>
        <el-checkbox label="选中且禁用" disabled></el-checkbox>
      </el-checkbox-group>
    </div>

    <div style="margin:20px">
      下拉菜单，可搜索，可多选
      <el-select
        v-model="value"
        filterable
        multiple
        placeholder="可搜索的选择框"
      >
        <el-option
          v-for="item in options"
          :key="item.value"
          :label="item.label"
          :value="item.value"
          :disabled="item.disabled"
        >
        </el-option>
      </el-select>

      <span class="demonstration">单选可搜索</span>
      <el-cascader
        placeholder="试试搜索：指南"
        :options="options2"
        filterable
      ></el-cascader>
      <span class="demonstration">多选可搜索</span>
      <el-cascader
        placeholder="试试搜索：指南"
        :options="options2"
        :props="{ multiple: true }"
        filterable
      ></el-cascader>
    </div>

    <div style="margin:20px">
      标签
      <el-tag
        v-for="item in items"
        :key="item.label"
        :type="item.type"
        :size="item.size"
        :closable="item.closable"
        effect="plain"
      >
        {{ item.label }}
      </el-tag>
    </div>

    <div style="margin:20px">
      表格
      <el-table
        :data="tableData"
        stripe
        style="width: 1000px"
        :default-sort="{ prop: 'date', order: 'descending' }"
      >
        <el-table-column type="selection" width="55" />
        <el-table-column
          prop="date"
          label="日期"
          sortable
          width="180"
          align="center"
          :filters="[
            { text: '2016-05-01', value: '2016-05-01' },
            { text: '2016-05-02', value: '2016-05-02' },
            { text: '2016-05-03', value: '2016-05-03' },
            { text: '2016-05-04', value: '2016-05-04' },
          ]"
          :filter-method="filterHandler"
        />
        <el-table-column
          prop="name"
          label="姓名"
          sortable
          width="180"
          align="center"
        />
        <el-table-column
          width="300"
          prop="address"
          label="地址"
          align="center"
        />
        <el-table-column
          width="300"
          prop="address"
          label="地址"
          align="center"
        />
        <el-table-column
          width="300"
          fixed="right"
          prop="address"
          label="地址"
          align="center"
        />
      </el-table>
    </div>

    <div>
      翻页
      <el-pagination
        :page-sizes="[50, 100, 200, 400]"
        :page-size="100"
        background
        layout="prev, pager, next, total, jumper, sizes"
        :total="1000"
        prev-text="上一页"
        next-text="下一页"
      />
    </div>

    <div>
      面包屑
      <el-breadcrumb separator="·">
        <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
        <el-breadcrumb-item><a href="/">活动管理</a></el-breadcrumb-item>
        <el-breadcrumb-item>活动列表</el-breadcrumb-item>
        <el-breadcrumb-item>活动详情</el-breadcrumb-item>
      </el-breadcrumb>
    </div>
    <div style="margin:20px">
      开关
      <el-switch v-model="switchValue"> </el-switch>
    </div>

    <div>
      滑杆
      <el-slider v-model="sliderValue" range :max="50" :min="5" />
      {{ sliderValue[0] + "~" + sliderValue[1] }}
    </div>

    <div>
      文字按钮
      <el-button type="text">新建项目</el-button>
    </div>

    <div>
      Tab
      <el-tabs type="border-card">
        <el-tab-pane label="用户管理">用户管理</el-tab-pane>
        <el-tab-pane label="配置管理">配置管理</el-tab-pane>
        <el-tab-pane label="角色管理">角色管理</el-tab-pane>
        <el-tab-pane label="定时任务补偿">定时任务补偿</el-tab-pane>
      </el-tabs>
    </div>

    <div>
      tips
      <el-tooltip
        class="item"
        effect="dark"
        content="Top Center 提示文字"
        placement="top"
      >
        <el-button>上边</el-button>
      </el-tooltip>
      <el-tooltip
        class="item"
        effect="light"
        content="Bottom Center 提示文字"
        placement="bottom"
      >
        <el-button>下边</el-button>
      </el-tooltip>
    </div>

    <div>
      步骤条
      <el-steps :active="active" finish-status="success">
        <el-step title="1.选择组卷方式"></el-step>
        <el-step title="2.选择组卷题目"></el-step>
        <el-step title="3.设置抽题方式"></el-step>
        <el-step title="4.设置试卷参数"></el-step>
        <el-step title="5.完成"></el-step>
      </el-steps>
      <el-button style="margin-top: 12px;" @click="next">下一步</el-button>
    </div>

    <div>
      消息提示
      <el-button :plain="true" @click="open2">成功</el-button>
      <el-button :plain="true" @click="open3">警告</el-button>
      <el-button :plain="true" @click="open1">消息</el-button>
      <el-button :plain="true" @click="open4">错误</el-button>
    </div>

    <div>
      日期时间选择
      <el-date-picker
        v-model="dateTimeValue"
        type="datetime"
        placeholder="选择日期时间"
        align="right"
        :picker-options="pickerOptions"
      />
      <el-date-picker
        v-model="dateTimeValue2"
        type="datetimerange"
        :picker-options="pickerOptions2"
        range-separator="至"
        start-placeholder="开始日期"
        end-placeholder="结束日期"
        align="right"
      >
      </el-date-picker>
    </div>

    <div>
      链接
      <el-link
        :underline="false"
        href="https://element.eleme.io"
        target="_blank"
        >https://element.eleme.io</el-link
      >
      <br />
      链接
      <el-link :underline="false" type="primary"
        >https://element.eleme.io</el-link
      >
    </div>

    <div>
      icon文字按钮
      <el-button type="text" icon="el-icon-circle-plus-outline"
        >添加新规则</el-button
      >
    </div>

    <div>
      loading
      <el-button
        type="primary"
        @click="openFullScreen1"
        v-loading.fullscreen.lock="fullscreenLoading"
        element-loading-text="加载中，请稍后"
      >
        指令方式
      </el-button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      input: "Hello Element UI!",
      input2: "",
      switchValue: true,
      radio: "2",
      checkList: ["选中且禁用", "复选框 A"],
      options: [
        {
          value: "选项1",
          label: "黄金糕",
        },
        {
          value: "选项2",
          label: "双皮奶",
          disabled: true,
        },
        {
          value: "选项3",
          label: "蚵仔煎",
        },
        {
          value: "选项4",
          label: "龙须面",
        },
        {
          value: "选项5",
          label: "北京烤鸭",
        },
      ],
      value: "",

      options2: [
        {
          value: "zhinan",
          label: "指南",
          children: [
            {
              value: "shejiyuanze",
              label: "设计原则",
              children: [
                {
                  value: "yizhi",
                  label: "一致",
                },
                {
                  value: "fankui",
                  label: "反馈",
                },
                {
                  value: "xiaolv",
                  label: "效率",
                },
                {
                  value: "kekong",
                  label: "可控",
                },
              ],
            },
            {
              value: "daohang",
              label: "导航",
              children: [
                {
                  value: "cexiangdaohang",
                  label: "侧向导航",
                },
                {
                  value: "dingbudaohang",
                  label: "顶部导航",
                },
              ],
            },
          ],
        },
        {
          value: "zujian",
          label: "组件",
          children: [
            {
              value: "basic",
              label: "Basic",
              children: [
                {
                  value: "layout",
                  label: "Layout 布局",
                },
                {
                  value: "color",
                  label: "Color 色彩",
                },
                {
                  value: "typography",
                  label: "Typography 字体",
                },
                {
                  value: "icon",
                  label: "Icon 图标",
                },
                {
                  value: "button",
                  label: "Button 按钮",
                },
              ],
            },
            {
              value: "form",
              label: "Form",
              children: [
                {
                  value: "radio",
                  label: "Radio 单选框",
                },
                {
                  value: "checkbox",
                  label: "Checkbox 多选框",
                },
                {
                  value: "input",
                  label: "Input 输入框",
                },
                {
                  value: "input-number",
                  label: "InputNumber 计数器",
                },
                {
                  value: "select",
                  label: "Select 选择器",
                },
                {
                  value: "cascader",
                  label: "Cascader 级联选择器",
                },
                {
                  value: "switch",
                  label: "Switch 开关",
                },
                {
                  value: "slider",
                  label: "Slider 滑块",
                },
                {
                  value: "time-picker",
                  label: "TimePicker 时间选择器",
                },
                {
                  value: "date-picker",
                  label: "DatePicker 日期选择器",
                },
                {
                  value: "datetime-picker",
                  label: "DateTimePicker 日期时间选择器",
                },
                {
                  value: "upload",
                  label: "Upload 上传",
                },
                {
                  value: "rate",
                  label: "Rate 评分",
                },
                {
                  value: "form",
                  label: "Form 表单",
                },
              ],
            },
            {
              value: "data",
              label: "Data",
              children: [
                {
                  value: "table",
                  label: "Table 表格",
                },
                {
                  value: "tag",
                  label: "Tag 标签",
                },
                {
                  value: "progress",
                  label: "Progress 进度条",
                },
                {
                  value: "tree",
                  label: "Tree 树形控件",
                },
                {
                  value: "pagination",
                  label: "Pagination 分页",
                },
                {
                  value: "badge",
                  label: "Badge 标记",
                },
              ],
            },
            {
              value: "notice",
              label: "Notice",
              children: [
                {
                  value: "alert",
                  label: "Alert 警告",
                },
                {
                  value: "loading",
                  label: "Loading 加载",
                },
                {
                  value: "message",
                  label: "Message 消息提示",
                },
                {
                  value: "message-box",
                  label: "MessageBox 弹框",
                },
                {
                  value: "notification",
                  label: "Notification 通知",
                },
              ],
            },
            {
              value: "navigation",
              label: "Navigation",
              children: [
                {
                  value: "menu",
                  label: "NavMenu 导航菜单",
                },
                {
                  value: "tabs",
                  label: "Tabs 标签页",
                },
                {
                  value: "breadcrumb",
                  label: "Breadcrumb 面包屑",
                },
                {
                  value: "dropdown",
                  label: "Dropdown 下拉菜单",
                },
                {
                  value: "steps",
                  label: "Steps 步骤条",
                },
              ],
            },
            {
              value: "others",
              label: "Others",
              children: [
                {
                  value: "dialog",
                  label: "Dialog 对话框",
                },
                {
                  value: "tooltip",
                  label: "Tooltip 文字提示",
                },
                {
                  value: "popover",
                  label: "Popover 弹出框",
                },
                {
                  value: "card",
                  label: "Card 卡片",
                },
                {
                  value: "carousel",
                  label: "Carousel 走马灯",
                },
                {
                  value: "collapse",
                  label: "Collapse 折叠面板",
                },
              ],
            },
          ],
        },
        {
          value: "ziyuan",
          label: "资源",
          children: [
            {
              value: "axure",
              label: "Axure Components",
            },
            {
              value: "sketch",
              label: "Sketch Templates",
            },
            {
              value: "jiaohu",
              label: "组件交互文档",
            },
          ],
        },
      ],
      items: [
        { type: "", label: "标签一", size: "", closable: true },
        { type: "success", label: "标签二", size: "medium", closable: true },
        { type: "info", label: "标签三", size: "small", closable: true },
        { type: "danger", label: "标签四", size: "mini", closable: true },
        { type: "warning", label: "标签五", closable: false },
      ],
      sliderValue: [12, 24],
      active: 0,
      tableData: [
        {
          date: "2016-05-02",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1518 弄",
        },
        {
          date: "2016-05-04",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1517 弄",
        },
        {
          date: "2016-05-01",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1519 弄",
        },
        {
          date: "2016-05-03",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1516 弄",
        },
      ],
      fullscreenLoading: false,

      pickerOptions: {
        shortcuts: [
          {
            text: "今天",
            onClick(picker) {
              picker.$emit("pick", new Date());
            },
          },
          {
            text: "昨天",
            onClick(picker) {
              const date = new Date();
              date.setTime(date.getTime() - 3600 * 1000 * 24);
              picker.$emit("pick", date);
            },
          },
          {
            text: "一周前",
            onClick(picker) {
              const date = new Date();
              date.setTime(date.getTime() - 3600 * 1000 * 24 * 7);
              picker.$emit("pick", date);
            },
          },
        ],
      },
      pickerOptions2: {
        shortcuts: [
          {
            text: "最近一周",
            onClick(picker) {
              const end = new Date();
              const start = new Date();
              start.setTime(start.getTime() - 3600 * 1000 * 24 * 7);
              picker.$emit("pick", [start, end]);
            },
          },
          {
            text: "最近一个月",
            onClick(picker) {
              const end = new Date();
              const start = new Date();
              start.setTime(start.getTime() - 3600 * 1000 * 24 * 30);
              picker.$emit("pick", [start, end]);
            },
          },
          {
            text: "最近三个月",
            onClick(picker) {
              const end = new Date();
              const start = new Date();
              start.setTime(start.getTime() - 3600 * 1000 * 24 * 90);
              picker.$emit("pick", [start, end]);
            },
          },
        ],
      },
      dateTimeValue: "",
      dateTimeValue2: "",
    };
  },
  methods: {
    openFullScreen1() {
      this.fullscreenLoading = true;
      setTimeout(() => {
        this.fullscreenLoading = false;
      }, 2000);
    },
    next() {
      if (this.active++ > 4) this.active = 0;
    },
    open1() {
      this.$message("这是一条消息提示");
    },
    open2() {
      this.$message({
        message: "恭喜你，这是一条成功消息",
        type: "success",
      });
    },

    open3() {
      this.$message({
        message: "警告哦，这是一条警告消息",
        type: "warning",
      });
    },
    open4() {
      this.$message.error("错了哦，这是一条错误消息");
    },
    filterHandler(value, row, column) {
      const property = column["property"];
      return row[property] === value;
    },
  },
};
</script>
<style scoped>
div {
  margin: 20px;
}
.warning {
  color: red;
}
</style>
