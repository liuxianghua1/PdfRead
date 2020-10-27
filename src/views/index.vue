<template>
  <div>
    <div class="demo-image">
      <div class="block" v-for="fit in fits" :key="fit">
        <el-image :src="readLink" :fit="fit"></el-image>
      </div>
    </div>
    <div>
      <el-button type="primary" @click="back()">上一页</el-button>
      <span>当前页码:{{ this.readNum }}</span>
      <el-button type="primary" style="float: right" @click="next()"
        >下一页</el-button
      >
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      fits: ["fill"],
      readNum: Number(localStorage.getItem("page")),
      readLink: "",
    };
  },
  methods: {
    fetch() {
      this.readLink = localStorage.getItem("num");
    },
    next() {
      let nextNum = (this.readNum += 1);
      this.readNum = nextNum;
      localStorage.setItem("page", nextNum);
      localStorage.setItem(
        "num",
        "http://thumb.1010pic.com/dmt/diandu3/file/book/1738/" +
          nextNum +
          ".jpg"
      );
      this.readLink = localStorage.getItem("num");
    },
    back() {
      let nextNum = (this.readNum -= 1);
      this.readNum = nextNum;
      localStorage.setItem("page", nextNum);
      localStorage.setItem(
        "num",
        "http://thumb.1010pic.com/dmt/diandu3/file/book/1738/" +
          nextNum +
          ".jpg"
      );
      this.readLink = localStorage.getItem("num");
    },
  },
  created() {
    this.fetch();
    document.onkeydown = e => {
      //事件对象兼容
      let e1 =
        e || event || window.event || arguments.callee.caller.arguments[0];
      //键盘按键判断:左箭头-37;上箭头-38；右箭头-39;下箭头-40
      if (e1 && e1.keyCode == 37) {
       this.back()
      } else if (e1 && e1.keyCode == 39) {
       this.next()
      }
    };
  },
};
</script>