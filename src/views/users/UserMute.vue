<template>
  <div>
    <a-card
      style="margin-top: 24px"
      :bordered="false"
      title="用户列表">
      <p>用户id：</p>
      <p class="lineStyle">
        <a-form-item>
          <a-input v-model="queryId" placeholder="" style="flex:1"/>
        </a-form-item>
        <a-button type="primary" @click="search" class="searchBtn">查询</a-button>
        <a-button @click="reset" class="searchBtn">重置</a-button>
      </p>
      <a-list
      size="large">
        <a-list-item :key="item.id" v-for="(item, index) in data" v-show="index >= currentlySize && index < pageSize">
          <div class="list-content">
            <div class="list-content-item">
              <span>id</span>
              <p>{{ item.id }}</p>
            </div>
          </div>
          <div class="list-content">
            <div class="list-content-item">
              <span>状态</span>
              <p v-text="item.userState == 0? '正常' : '禁言'"></p>
            </div>
          </div>
          <div slot="actions">
            <a @click="mute(item.id, item.userState, index)" v-text="item.userState == 0? '禁言' : '取消禁言'"></a>
          </div>
           <a-list-item-meta>
            <a-avatar slot="avatar" size="large" shape="square" :src="item.avatar"/>
            <a slot="title">{{ item.title }}</a>
          </a-list-item-meta>
        </a-list-item>
      </a-list>
    </a-card>
    <a-pagination showQuickJumper :defaultCurrent="1" :total="totalSize" @change="onChange" :pageSize="1"></a-pagination>
    <operate-modal ref="operate" @isok="okOperate"/>
  </div>
</template>

<script>
import OperateModal from '../users/OperateModal'
const data = []
data.push({
  id:1,
  title: 'Alipay',
  avatar: 'https://gw.alipayobjects.com/zos/rmsportal/WdGqmHpayyMjiEhcKoVE.png',
  description: '那是一种内在的东西， 他们到达不了，也无法触及的',
  owner: '付晓晓',
  startAt: '2018-07-26 22:44',
  userState:0
})
data.push({
  id:2,
  title: 'Angular',
  avatar: 'https://gw.alipayobjects.com/zos/rmsportal/zOsKZmFRdUtvpqCImOVY.png',
  description: '希望是一个好东西，也许是最好的，好东西是不会消亡的',
  owner: '曲丽丽',
  startAt: '2018-07-26 22:44',
  userState:0
})
data.push({
  id:3,
  title: 'Ant Design',
  avatar: 'https://gw.alipayobjects.com/zos/rmsportal/dURIMkkrRFpPgTuzkwnB.png',
  description: '生命就像一盒巧克力，结果往往出人意料',
  owner: '林东东',
  startAt: '2018-07-26 22:44',
  userState:0
})
data.push({
  id:4,
  title: '管理系统平台',
  avatar: 'https://gw.alipayobjects.com/zos/rmsportal/sfjbOqnsXXJgNCjCzDBL.png',
  description: '城镇中有那么多的酒馆，她却偏偏走进了我的酒馆',
  owner: '周星星',
  startAt: '2018-07-26 22:44',
  userState:0
})
data.push({
  id:5,
  title: 'Bootstrap',
  avatar: 'https://gw.alipayobjects.com/zos/rmsportal/siCrBXXhmvTQGWPNLBow.png',
  description: '那时候我只会想自己想要什么，从不想自己拥有什么',
  owner: '吴加好',
  startAt: '2018-07-26 22:44',
  userState:0
})
data.push({
  id:6,
  title: 'Alipay',
  avatar: 'https://gw.alipayobjects.com/zos/rmsportal/WdGqmHpayyMjiEhcKoVE.png',
  description: '那是一种内在的东西， 他们到达不了，也无法触及的',
  owner: '付晓晓',
  startAt: '2018-07-26 22:44',
  userState:0
})
data.push({
  id:7,
  title: 'Angular',
  avatar: 'https://gw.alipayobjects.com/zos/rmsportal/zOsKZmFRdUtvpqCImOVY.png',
  description: '希望是一个好东西，也许是最好的，好东西是不会消亡的',
  owner: '曲丽丽',
  startAt: '2018-07-26 22:44',
  userState:0
})
data.push({
  id:8,
  title: 'Ant Design',
  avatar: 'https://gw.alipayobjects.com/zos/rmsportal/dURIMkkrRFpPgTuzkwnB.png',
  description: '生命就像一盒巧克力，结果往往出人意料',
  owner: '林东东',
  startAt: '2018-07-26 22:44',
  userState:0
})
data.push({
  id:9,
  title: '管理系统平台',
  avatar: 'https://gw.alipayobjects.com/zos/rmsportal/sfjbOqnsXXJgNCjCzDBL.png',
  description: '城镇中有那么多的酒馆，她却偏偏走进了我的酒馆',
  owner: '周星星',
  startAt: '2018-07-26 22:44',
  userState:0
})
data.push({
  id:10,
  title: 'Bootstrap',
  avatar: 'https://gw.alipayobjects.com/zos/rmsportal/siCrBXXhmvTQGWPNLBow.png',
  description: '那时候我只会想自己想要什么，从不想自己拥有什么',
  owner: '吴加好',
  startAt: '2018-07-26 22:44',
  userState:0
})
data.push({
  id:11,
  title: 'Alipay',
  avatar: 'https://gw.alipayobjects.com/zos/rmsportal/WdGqmHpayyMjiEhcKoVE.png',
  description: '那是一种内在的东西， 他们到达不了，也无法触及的',
  owner: '付晓晓',
  startAt: '2018-07-26 22:44',
  userState:0
})
data.push({
  id:12,
  title: 'Angular',
  avatar: 'https://gw.alipayobjects.com/zos/rmsportal/zOsKZmFRdUtvpqCImOVY.png',
  description: '希望是一个好东西，也许是最好的，好东西是不会消亡的',
  owner: '曲丽丽',
  startAt: '2018-07-26 22:44',
  userState:0
})
data.push({
  id:13,
  title: 'Ant Design',
  avatar: 'https://gw.alipayobjects.com/zos/rmsportal/dURIMkkrRFpPgTuzkwnB.png',
  description: '生命就像一盒巧克力，结果往往出人意料',
  owner: '林东东',
  startAt: '2018-07-26 22:44',
  userState:0
})
data.push({
  id:14,
  title: '管理系统平台',
  avatar: 'https://gw.alipayobjects.com/zos/rmsportal/sfjbOqnsXXJgNCjCzDBL.png',
  description: '城镇中有那么多的酒馆，她却偏偏走进了我的酒馆',
  owner: '周星星',
  startAt: '2018-07-26 22:44',
  userState:0
})
data.push({
  id:15,
  title: 'Bootstrap',
  avatar: 'https://gw.alipayobjects.com/zos/rmsportal/siCrBXXhmvTQGWPNLBow.png',
  description: '那时候我只会想自己想要什么，从不想自己拥有什么',
  owner: '吴加好',
  startAt: '2018-07-26 22:44',
  userState:0
})

export default {
  name: 'UserMute',
  data () {
    return {
      data,
      status: 'all',
      queryId: "",
      pageSize:5,
      currentlySize: 0,
      pageShowSize:5,
      totalSize: 3,//总页数，需用总条数/每页显示数
      checkIndex: "",
      checkUserState: ""
    }
  },
  components: {
    OperateModal
  },
  methods: {
    search: function(){
      //调用接口
      console.log(this.queryId)
      this.data = [{title: 'Bootstrap',
      avatar: 'https://gw.alipayobjects.com/zos/rmsportal/siCrBXXhmvTQGWPNLBow.png',
      description: '那时候我只会想自己想要什么，从不想自己拥有什么',
      owner: '吴加好',
      startAt: '2018-07-26 22:44',
      progress: {
        status: 'exception',
        value: 100
      }}];
    },
    reset: function(){
        this.queryId = "";
        this.data = data;
    },
    okOperate: function(){
      setTimeout(() => {
        this.$refs.operate.close();
        console.log(this.checkIndex)
        console.log(this.checkUserState)
        this.data[this.checkIndex].userState = !this.userState;
      }, 2000);
    },
    mute: function(id, userState, index){
      console.log(id)
      console.log(userState)
      this.checkIndex = index;
      this.checkUserState = userState;
      
      this.$refs.operate.open('是否要禁言该用户？', '正在处理...');
    },
     onChange(pageNumber) {
        this.pageSize = pageNumber * this.pageShowSize;
        this.currentlySize =  this.pageSize - this.pageShowSize;
        console.log('currentlySize: ', this.currentlySize);
        console.log(' this.pageSize: ',  this.pageSize);
        console.log('Page: ', pageNumber);
    }
  }
}
</script>

<style lang="less" scoped>
    .ant-pagination{
      text-align: right;
      margin-top: 10px;
    }
    .ant-form-item{
      width: 100%; 
      margin-bottom: 0;
    }
    .lineStyle{
      display: flex;
      align-items: center;
    }
    .searchBtn{
      margin-left: 20px;
    }
    .ant-list-item-meta{
      align-items: center;
    }
    .ant-avatar-lg {
        width: 48px;
        height: 48px;
        line-height: 48px;
    }

    .list-content-item {
        color: rgba(0, 0, 0, .45);
        display: inline-block;
        vertical-align: middle;
        font-size: 14px;
        margin-right: 240px;
        span {
            line-height: 20px;
        }
        p {
            margin-top: 4px;
            margin-bottom: 0;
            line-height: 22px;
        }
    }
</style>
