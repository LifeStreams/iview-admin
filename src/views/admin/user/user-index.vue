<style lang="less">
@import "../../../styles/common.less";
@import "./../components/table.less";
</style>
<template>
    <div>       
                <Card>
                    <p slot="title">
                        <Icon type="pinpoint"></Icon>
                        用户列表
                    </p>
                    <Row>
                      <Col span="18">
                        <Input v-model="searchmodel" icon="search" @on-click="handleSearch1" placeholder="请输入姓名搜索..." style="width: 200px" />
                      </Col>
                      <Col span="6">                      
                            <Button type="primary" @click="addUserModel = true" long shape="circle" size="small" icon="plus-round" style="float:right;margin-top:5px;margin-left:-5px"></Button>
                            <Modal v-model="addUserModel" title="Add">
                              <p>123123</p>
                            </Modal>
                      </Col>                  
                    </Row>
                    <Row class="margin-top-10 searchable-table-con1">
                        <Table :columns="tableTitle" :data="users" style="width: 100%;"></Table>                        
                    </Row>
                </Card>            
    </div>
</template>

<script>
import * as table from "./mockdata/usertable.js";
import util from "@/libs/util.js";
export default {
  name: "editable-table",
  data() {
    return {
      addUserModel: false,
      tableTitle: [
        {
          title: "账号",
          align: "center",
          key: "account",
          editable: true
        },
        {
          title: "姓名",
          align: "center",
          key: "userName",
          editable: true
        },
        {
          title: "性别",
          align: "center",
          key: "gender"
        },
        {
          title: "邮箱",
          align: "center",
          key: "email",
          editable: true
        },
        {
          title: "类型",
          align: "center",
          key: "type",
          editable: true
        },
        {
          title: "锁定",
          align: "center",
          key: "lock",
          render: (h, params) => {
            return h("i-switch", {
              props: {
                value: params.row.lock === "1",
                "true-value": "1",
                "false-value": "0"
              },
              on: {
                "on-change": value => {
                  let datas = new URLSearchParams();
                  datas.append("account", params.row.account);
                  datas.append("lock", value);
                  util
                    .ajax("lock", {
                      method: "post",
                      data: datas
                    })
                    .then(response => {
                      this.$Message.success(
                        params.row.account +
                          "用户" +
                          (value == "1" ? "锁定" : "解锁") +
                          "成功!"
                      );
                    })
                    .catch(() => {
                      this.$Message.error(params.row.account + "用户锁定失败!");
                    });
                }
              }
            });
          }
        },
        {
          title: "操作",
          align: "center",
          width: 200,
          key: "handle",
          render: (h, params) => {
            return [
              h(
                "Button",
                {
                  props: {
                    type: "error",
                    size: "small"
                  },
                  style: {
                    marginRight: "3px"
                  },
                  on: {
                    click: () => {}
                  }
                },
                "删除"
              ),
              h(
                "Button",
                {
                  props: {
                    type: "primary",
                    size: "small"
                  },
                  style: {
                    marginRight: "3px"
                  },
                  on: {
                    click: () => {}
                  }
                },
                "编辑"
              )
            ];
          }
        }
      ],
      searchmodel: "",
      users: []
    };
  },
  methods: {
    init() {
      this.users = table.mockData;
      // util
      //   .ajax("user")
      //   .then(response => {
      //     this.users = response.data.result;
      //   })
      //   .catch(() => {
      //     this.$Message.error("服务器网络异常");
      //   });
    },
    handleSearch1() {
      this.$Message.success("搜索");
    },
    handleNetConnect(state) {
      this.breakConnect = state;
    },
    handleLowSpeed(state) {
      this.lowNetSpeed = state;
    },
    getCurrentData() {
      this.showCurrentTableData = true;
    },
    handleDel(val, index) {
      this.$Message.success("删除了第" + (index + 1) + "行数据");
    },
    handleChange(val, index) {
      this.$Message.success("修改了第" + (index + 1) + "行数据");
    }
  },
  mounted() {
    this.init();
  }
};
</script>
