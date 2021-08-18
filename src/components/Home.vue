<template>
  <div>
    <Menu mode="horizontal" theme="primary" active-name="1">
      <MenuItem name="1">
        <Icon type="ios-paper" />
        聚合图床 PoPic
      </MenuItem>
      <div style="float: right">
        <MenuItem name="2">
          <Icon type="ios-people" />
          用户管理
        </MenuItem>
        <Submenu name="3">
          <template slot="title">
            <Icon type="ios-stats" />
            统计分析
          </template>
          <MenuGroup title="使用">
            <MenuItem name="3-1">新增和启动</MenuItem>
            <MenuItem name="3-2">活跃分析</MenuItem>
            <MenuItem name="3-3">时段分析</MenuItem>
          </MenuGroup>
          <MenuGroup title="留存">
            <MenuItem name="3-4">用户留存</MenuItem>
            <MenuItem name="3-5">流失用户</MenuItem>
          </MenuGroup>
        </Submenu>
        <MenuItem name="4">
          <Icon type="ios-construct" />
          综合设置
        </MenuItem>
      </div>
    </Menu>
    <!-- <po-pic-menu ref="PoPicMenu"></po-pic-menu> -->
    <div class="container">
      <Alert type="success"
        >注意：限制每日上传100张，单张图片不能超过5M，上传的图片将公开显示，使用之前请先阅读《使用协议》</Alert
      >
      <Upload multiple type="drag" paste action="">
        <div style="padding: 20px 0">
          <Icon type="ios-cloud-upload" size="52" style="color: #3399ff"></Icon>
          <p>将图片拖拽到此处，支持Ctrl+V粘贴上传</p>
        </div>
      </Upload>
      <Card>
        <p slot="title">上传位置</p>
        <div>
          <label for="">公共图床：</label>
          <Tag size="medium" color="success">本地</Tag>
          <Tag closable @on-close="handleCloseTag" size="medium" color="success"
            >sm.ms</Tag
          >
          <Tag size="medium"
            >imgurl
            <span style="cursor: pointer">&nbsp;<Icon type="ios-add" /></span>
          </Tag>
        </div>
        <div>
          <label for="">私人图床：</label>
          <Tag closable size="medium" color="primary">阿里云OSS</Tag>
          <Tag closable size="medium" color="primary">腾讯云COS</Tag>
          <Tag closable size="medium" color="primary">七牛云Qiniu</Tag>
          <Tag size="medium"
            >又拍云Upyun
            <span style="cursor: pointer">&nbsp;<Icon type="ios-add" /></span>
          </Tag>
        </div>
      </Card>
      <Card>
        <p slot="title">上传结果</p>
        <Row>
          <Col span="12">
            <div class="pic-load">
              <img
                src="//imgurl.ebans.net/imgs/2021/08/5f01edd3843a20f5.jpeg"
                alt=""
                class="img-view"
                @click="viewImage"
              />
              <!-- <img
                src="//ww1.sinaimg.cn/large/005JbynVgy1gthiknqqt2j30o01hcwhz.jpg"
                alt=""
                class="img-view"
                @click="viewImage"
              /> -->
              <!-- <img
                src="//imgurl.ebans.net/imgs/2019/07/a9fcdef1267b1209.png"
                alt=""
                class="img-view"
                @click="viewImage"
              /> -->
            </div>
          </Col>
          <Col span="12" style="align-self: center"
            ><div class="copy-area">
              <Input placeholder="Enter something..." class="copy-input" v-model="result.url"
                ><span slot="prepend">URL</span
                ><span slot="append" class="copy-icon" @click="copyText(result.url)"
                  ><Icon type="ios-copy" />复制</span
                ></Input
              >
              <Input placeholder="Enter something..." class="copy-input" v-model="result.html"
                ><span slot="prepend">HTML</span
                ><span slot="append" class="copy-icon" @click="copyText(result.html)"
                  ><Icon type="ios-copy" />复制</span
                ></Input
              >
              <Input placeholder="Enter something..." class="copy-input" v-model="result.markdown"
                ><span slot="prepend">Markdown</span
                ><span slot="append" class="copy-icon" @click="copyText(result.markdown)"
                  ><Icon type="ios-copy" />复制</span
                ></Input
              >
              <Input placeholder="Enter something..." class="copy-input" v-model="result.bbcode"
                ><span slot="prepend">BBCode</span
                ><span slot="append" class="copy-icon" @click="copyText(result.bbcode)"
                  ><Icon type="ios-copy" />复制</span
                ></Input
              ><Input placeholder="Enter something..." class="copy-input" v-model="result.deleteLink"
                ><span slot="prepend">Delete Link</span
                ><span slot="append" class="copy-icon" @click="copyText(result.deleteLink)"
                  ><Icon type="ios-copy" />复制</span
                ></Input
              >
            </div></Col
          >
        </Row>
      </Card>
      <Card style="margin-top: 10px">
        <p slot="title">注意事项</p>
        <div>
          <p>1、上传后返回的地址，是由后台依次请求上传位置而来。</p>
          <p>2、请求顺序影响图片返回速度，可在后台调整。</p>
        </div>
      </Card>
    </div>
  </div>
</template>

<script>
// import { PoPicMenu } from "./PoPicMenu.vue"
export default {
  // components: { PoPicMenu },
  data() {
    return {
      result: {
        url: '1',
        html: '2',
        markdown: '3',
        bbcode: '4',
        deleteLink: '5',
      }
    };
  },
  methods: {
    handleCloseTag(event, name) {
      console.log("123");
    },
    copyText(value) {
      if (!value) return false;
      this.$copyText(value).then((_) => {
        this.$Notice.success({
          title: "复制成功！",
          desc: value
        });
      });
    },
    viewImage(e) {
      window.open(e.target.src)
    }
  },
};
</script>

<style scoped>
.container {
  padding: 10px;
  margin-left: auto;
  margin-right: auto;
  max-width: 1200px;
}
.pic-load {
  text-align: center;
  padding: 20px;
}
.img-view {
  max-height: 400px;
  max-width: 100%;
  cursor: pointer;
}
.copy-area {
  max-width: 400px;
}
.copy-input {
  margin-top: 20px;
}
.copy-icon {
  cursor: pointer;
}
</style>