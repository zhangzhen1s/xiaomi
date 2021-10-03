<!--
 * @Description: 项目根组件
 * @Author: zhangzheng
 * @Date: 2021-08-07 16:23:00
 * @LastEditors: zhangzheng
 * @LastEditTime: 2021-10-1 13:14:48
 -->
<template>
  <div id="app" name="app">
    <el-container>
      <!-- 顶部导航栏 -->
      <div class="topbar">
        <div class="nav">
          <div class="topbar-nav">
            <a rel="nofollow" href="//www.mi.com/index.html">小米商城</a>
            <span class="sep">|</span>
            <a rel="nofollow" href="//www.miui.com" target="_blank">miui</a
            ><span class="sep">|</span>
            <a rel="nofollow" href="//iot.mi.com/" target="_blank">IOT</a>
            <span class="sep">|</span>
            <a rel="nofollow" href="//airstar.com/home" target="_blank"
              >天星数科</a
            >
            <span class="sep">|</span>
            <a rel="nofollow" href="//youpin.mi.com/" target="_blank">有品</a>
            <span class="sep">|</span>
            <a rel="nofollow" href="//xaioai.mi.com/" target="_blank"
              >小爱开放平台</a
            >
            <span class="sep">|</span>
            <a rel="nofollow" href="//qiye.mi.com/" target="_blank">企业团购</a>
            <span class="sep">|</span>
            <a
              rel="nofollow"
              href="//www.mi.com/aptitude/list/?id=88"
              target="_blank"
              >资质证照</a
            >
            <span class="sep">|</span>
            <a rel="nofollow" href="//www.mi.com/aptitude/list/" target="_blank"
              >协议规则</a
            >
            <span class="sep">|</span>
            <a rel="nofollow" href="//www.mi.com/appdownload/" target="_blank"
              >下载app</a
            >
            <span class="sep">|</span>
            <a
              rel="nofollow"
              href="//xiaomishare.mi.com/?from=micom"
              target="_blank"
              >智能生活</a
            >
            <span class="sep">|</span>
            <a rel="nofollow" href="#" target="_blank">Select Location</a>
            <span class="sep">|</span>
          </div>
          <ul>
            <li v-if="!this.$store.getters.getUser">
              <el-button type="text" @click="login">登录</el-button>
              <span class="sep">|</span>
              <el-button type="text" @click="register = true">注册</el-button>
            </li>
            <li v-else>
              欢迎
              <el-popover placement="top" width="180" v-model="visible">
                <p>确定退出登录吗？</p>
                <div style="text-align: right; margin: 10px 0 0">
                  <el-button size="mini" type="text" @click="visible = false"
                    >取消</el-button
                  >
                  <el-button type="primary" size="mini" @click="logout"
                    >确定</el-button
                  >
                </div>
                <el-button type="text" slot="reference">{{
                  this.$store.getters.getUser.userName
                }}</el-button>
              </el-popover>
            </li>
            <li>
              <router-link to="/order">我的订单</router-link>
            </li>
            <li>
              <router-link to="/collect">我的收藏</router-link>
            </li>
            <li :class="getNum > 0 ? 'shopCart-full' : 'shopCart'">
              <router-link to="/shoppingCart">
                <i class="el-icon-shopping-cart-full"></i> 购物车
                <span class="num">({{ getNum }})</span>
              </router-link>
            </li>
          </ul>
        </div>
      </div>
      <!-- 顶部导航栏END -->

      <!-- 顶栏容器 -->
      <el-header>
        <el-menu
          :default-active="activeIndex"
          class="el-menu-demo"
          mode="horizontal"
          active-text-color="#409eff"
          router
        >
          <div class="logo">
            <router-link to="/">
              <img
                src="./assets/imgs/logo.png"
                style="width: 60px; height: 60px"
                alt
              />
            </router-link>
          </div>
          <el-menu-item index="/">首页</el-menu-item>
          <el-menu-item index="/goods">全部商品</el-menu-item>
          <el-menu-item index="/about">关于我们</el-menu-item>

          <div class="so">
            <el-input placeholder="请输入搜索内容" v-model="search">
              <el-button
                slot="append"
                icon="el-icon-search"
                @click="searchClick"
              ></el-button>
            </el-input>
          </div>
        </el-menu>
      </el-header>
      <!-- 顶栏容器END -->

      <!-- 登录模块 -->
      <MyLogin></MyLogin>
      <!-- 注册模块 -->
      <MyRegister :register="register" @fromChild="isRegister"></MyRegister>

      <!-- 主要区域容器 -->
      <el-main>
        <keep-alive>
          <router-view></router-view>
        </keep-alive>
      </el-main>
      <!-- 主要区域容器END -->

      <!-- 底栏容器 -->
      <el-footer>
        <!-- 新增尾部服务 -->
        <div class="site-footer">
          <div class="contaniner w">
            <div class="footer-service">
              <ul class="list-service clearfix">
                <li class="a">
                  <a href="#"
                    ><em class="iconfont icon-weixiu"></em>预约维修服务</a
                  >
                </li>
                <li>
                  <a href="#"
                    ><em class="iconfont icon-7tiantuihuan"></em
                    >7天无理由退货</a
                  >
                </li>
                <li>
                  <a href="#"
                    ><em class="iconfont icon-15tianwuliyoutuihuo"></em
                    >15天免费退货</a
                  >
                </li>
                <li>
                  <a href="#"
                    ><em class="iconfont icon-liwuhuodong"></em>满69包邮</a
                  >
                </li>
                <li>
                  <a href="#"
                    ><em class="iconfont icon-dingwei"></em>520余家售后网点</a
                  >
                </li>
              </ul>
            </div>
            <div class="footer-links">
              <dl class="links">
                <dt>帮助中心</dt>
                <dd>账户管理</dd>
                <dd>购物指南</dd>
                <dd>订单操作</dd>
              </dl>
              <dl class="links">
                <dt>服务支持</dt>
                <dd>售后政策</dd>
                <dd>自助服务</dd>
                <dd>相关下载</dd>
              </dl>
              <dl class="links">
                <dt>线下门店</dt>
                <dd>小米之家</dd>
                <dd>服务网点</dd>
                <dd>授权体验店</dd>
              </dl>
              <dl class="links">
                <dt>关于小米</dt>
                <dd>了解小米</dd>
                <dd>加入小米</dd>
                <dd>投资者关系</dd>
                <dd>企业社会责任</dd>
                <dd>廉洁举报</dd>
              </dl>
              <dl class="links">
                <dt>关注我们</dt>
                <dd>新浪微博</dd>
                <dd>官方微信</dd>
                <dd>联系我们</dd>
                <dd>公益基金会</dd>
              </dl>
              <dl class="links">
                <dt>特色服务</dt>
                <dd>F码通道</dd>
                <dd>防伪查询</dd>
              </dl>
              <div class="contact">
                <p class="phone">400-100-5678</p>
                <p>8:00-18:00(仅收市话费)</p>
                <a href="#" class="btu"
                  ><em class="iconfont icon-liuyan">人工服务</em></a
                >
                <div class="follow">
                  关注小米:
                  <a
                    href="https://weibo.com/xiaomishangcheng"
                    target="_blank"
                    class="iconfont icon-xinlangweibo"
                  ></a>
                  <a href="#" id="wx" class="iconfont icon-weixin"></a>
                  <img id="J_followWxImg" style="display: none" />
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="site-info">
          <div class="contanier w">
            <div class="info-text">
              <div
                class="iconfont icon-icon-xiaomiguishu"
                style="
                  float: left;
                  margin-top: -15px;
                  width: 50px;
                  height: 50px;
                  font-size: 50px;
                  color: #ff6700; ;
                "
              ></div>
              <div class="wenzi">
                <p class="sites">
                  小米商城|MIUI|米家|米聊|多看|游戏|政企服务|小米天猫店|小米集团隐私政策|小米公司儿童信息保护规则|小米商城隐私政策|小米商城用户协议|问题反馈|Select
                  Location
                </p>
                <p class="sites">
                  北京互联网法院法律服务工作站|中国消费者协会|北京市消费者协会
                </p>
                <p>
                  © mi.com 京ICP证110507号 京ICP备10046444号
                  京公网安备11010802020134号 京网文[2020]0276-042号
                </p>
                <p>
                  （京）网械平台备字（2018）第00005号 互联网药品信息服务资格证
                  (京)-非经营性-2014-0090 营业执照 医疗器械质量公告
                </p>
                <p>
                  增值电信业务许可证 网络食品经营备案 京食药网食备202010048
                  食品经营许可证
                </p>
                <p>
                  违法和不良信息举报电话：171-5104-4404 知识产权侵权投诉
                  本网站所列数据，除特殊说明，所有数据均出自我司实验室测试
                </p>
              </div>
            </div>
            <div class="slogan">让全球每个人都能够享受科技带来的美好生活</div>
          </div>
        </div>
        <!-- 新增尾部服务end -->
      </el-footer>
      <!-- 底栏容器END -->
    </el-container>
  </div>
</template>

<script>
import { mapActions } from "vuex";
import { mapGetters } from "vuex";

export default {
  beforeUpdate() {
    this.activeIndex = this.$route.path;
  },
  data() {
    return {
      activeIndex: "", // 头部导航栏选中的标签
      search: "", // 搜索条件
      register: false, // 是否显示注册组件
      visible: false, // 是否退出登录
    };
  },
  created() {
    // 获取浏览器localStorage，判断用户是否已经登录
    if (localStorage.getItem("user")) {
      // 如果已经登录，设置vuex登录状态
      this.setUser(JSON.parse(localStorage.getItem("user")));
    }
  },
  computed: {
    ...mapGetters(["getUser", "getNum"]),
  },
  watch: {
    // 获取vuex的登录状态
    getUser: function (val) {
      if (val === "") {
        // 用户没有登录
        this.setShoppingCart([]);
      } else {
        // 用户已经登录,获取该用户的购物车信息
        this.$axios
          .post("/api/user/shoppingCart/getShoppingCart", {
            user_id: val.user_id,
          })
          .then((res) => {
            if (res.data.code === "001") {
              // 001 为成功, 更新vuex购物车状态
              this.setShoppingCart(res.data.shoppingCartData);
            } else {
              // 提示失败信息
              this.notifyError(res.data.msg);
            }
          })
          .catch((err) => {
            return Promise.reject(err);
          });
      }
    },
  },
  methods: {
    ...mapActions(["setUser", "setShowLogin", "setShoppingCart"]),
    login() {
      // 点击登录按钮, 通过更改vuex的showLogin值显示登录组件
      this.setShowLogin(true);
    },
    // 退出登录
    logout() {
      this.visible = false;
      // 清空本地登录信息
      localStorage.setItem("user", "");
      // 清空vuex登录信息
      this.setUser("");
      this.notifySucceed("成功退出登录");
    },
    // 接收注册子组件传过来的数据
    isRegister(val) {
      this.register = val;
    },
    // 点击搜索按钮
    searchClick() {
      if (this.search != "") {
        // 跳转到全部商品页面,并传递搜索条件
        this.$router.push({ path: "/goods", query: { search: this.search } });
        this.search = "";
      }
    },
  },
};
</script>

<style>
/* 全局CSS */
* {
  padding: 0;
  margin: 0;
  border: 0;
  list-style: none;
}
#app .el-header {
  padding: 0;
}
#app .el-main {
  min-height: 300px;
  padding: 20px 0;
}
#app .el-footer {
  padding: 0;
}
a,
a:hover {
  text-decoration: none;
}
/* 全局CSS END */

/* 顶部导航栏CSS */
.topbar {
  height: 40px;
  background-color: #3d3d3d;
  margin-bottom: 20px;
}
.topbar .nav {
  width: 1225px;
  margin: 0 auto;
}
/* 新增顶部导航栏 */
.nav .topbar-nav {
  float: left;
}
.nav a {
  color: #b0b0b0;
  font-size: 12px;
  line-height: 40px;
  display: inline-block;
}
.nav .sep {
  margin: 0 0.3em;
  color: #424242;
}
.nav a:hover {
  color: white;
}
/* 新增顶部导航栏end */
.topbar .nav ul {
  float: right;
}
.topbar .nav li {
  float: left;
  height: 40px;
  color: #b0b0b0;
  font-size: 14px;
  text-align: center;
  line-height: 40px;
  margin-left: 20px;
}
.topbar .nav .sep {
  color: #b0b0b0;
  font-size: 12px;
  margin: 0 5px;
}
.topbar .nav li .el-button {
  color: #b0b0b0;
}
.topbar .nav .el-button:hover {
  color: #fff;
}
.topbar .nav li a {
  color: #b0b0b0;
}
.topbar .nav a:hover {
  color: #fff;
}
.topbar .nav .shopCart {
  width: 120px;
  background: #424242;
}
.topbar .nav .shopCart:hover {
  background: #fff;
}
.topbar .nav .shopCart:hover a {
  color: #ff6700;
}
.topbar .nav .shopCart-full {
  width: 120px;
  background: #ff6700;
}
.topbar .nav .shopCart-full a {
  color: white;
}

/* 顶部导航栏CSS END */

/* 顶栏容器CSS */
.el-header .el-menu {
  max-width: 1225px;
  margin: 0 auto;
}
.el-header .logo {
  height: 60px;
  width: 189px;
  float: left;
  margin-right: 100px;
}
.el-header .so {
  margin-top: 10px;
  width: 300px;
  float: right;
}
/* 顶栏容器CSS END */

/* 底栏容器CSS */

/* 新增尾部css */
.stie-footer {
  width: 1349px;
}
.container {
  width: 1226px;
  margin-right: auto;
  margin-left: auto;
}
.footer-service {
  width: 1226px;
  height: 80px;
}
.site-footer .footer-service {
  padding: 27px 0;
  border-bottom: 1px solid #e0e0e0;
}
.footer-service .list-service {
  width: 1226px;
  height: 25px;
  list-style-type: none;
}
.footer-service .list-service li {
  float: left;
  width: 19.8%;
  height: 25px;
  font-size: 16px;
  line-height: 25px;
  text-align: center;
  border-left: 1px solid #e0e0e0;
}
.footer-service .list-service .a {
  border-left: 0px;
}
.footer-service .list-service em {
  font-size: 25px;
  margin-right: 5px;
  margin-bottom: 2px;
}
.footer-links {
  height: 252px;
  padding: 40px 0;
}
.footer-links .links {
  display: block;
  float: left;
  width: 160px;
  margin: 0;
}
.footer-links .links dt {
  margin: -1px 0 26px;
  font-size: 14px;
  line-height: 1.25;
  color: #424242;
}
.footer-links .links dd {
  margin: 10px 0 0;
  font-size: 12px;
}
.footer-links .links dd:hover {
  color: #ff6700;
}
.footer-links .contact {
  float: right;
  width: 251px;
  border-left: 1px solid #e0e0e0;
  text-align: center;
  color: #616161;
}
.footer-links .contact .phone {
  font-size: 22px;
  line-height: 1;
  color: #ff6700;
}
.footer-links .contact .btu {
  display: inline-block;
  width: 118px;
  height: 28px;
  font-size: 12px;
  line-height: 28px;
  border: 1px solid #ff6700;
  background: #fff;
  color: #ff6700;
  margin: 5px 0;
}
.footer-links .contact .follow a {
  font-size: 20px;
}
.footer-links .contact p {
  margin: 5px 0;
}
.site-info {
  padding: 30px 0;
  font-size: 12px;
  height: 266px;
  background: #fafafa;
}
.site-info .info-text {
  height: 110px;
  color: #b0b0b0;
}
.site-info .info-text .sites {
  width: 1159px;
  height: 19px;
  line-height: 18px;
  font-size: 12px;
  color: #333;
}
.site-info .info-text p {
  margin-left: 60px;
}
.slogan {
  text-align: center;
  margin-top: 30px;
  color: #b0b0b0;
  font-size: 20px;
}

/* 底栏容器CSS END */
</style>