<template>
  <div id="app">
    <StyleEditor ref="styleEditor" :code="currentStyle"></StyleEditor>
    <ResumeEditor ref="resumeEditor" :markdown="currentMarkdown" :enableHtml="enableHtml"></ResumeEditor>
  </div>
</template>

<script>
import StyleEditor from "./components/StyleEditor";
import ResumeEditor from "./components/ResumeEditor";
import "./assets/reset.css";

export default {
  name: "app",
  components: {
    StyleEditor,
    ResumeEditor
  },
  data() {
    return {
      // 动画延时
      interval: 3,
      currentStyle: "",
      enableHtml: false,
      fullStyle: [
        `/*
* Inspired by http://strml.net/
* 源码地址 https://github.com/Phoenix500526/Animation-Resume.git
* 大家好，我是Phoenix。
* 我来写一份简历！
*/

/* 给所有元素加上过渡效果 */
* {
  transition: all .1s;
}
/* 设置背景颜色 */
html {
  color: rgb(222,222,222); background: rgb(0,0,0);
}

/* 设置边框 */
.styleEditor {
  padding: .5em;
  border: 1px solid;
  margin: .5em;
  overflow: auto;
  width: 45vw; height: 90vh;
  /* background: rgb(20,20,20); */
}
/* 代码高亮 */
.token.selector{ color: rgb(250,0,0); }
.token.property{ color: rgb(247,151,29); }
.token.punctuation{ color: yellow; }
.token.function{ color: rgb(42,161,152); }

/* 加3D效果 */
html{
  perspective: 1000px;
}
.styleEditor {
  position: fixed; left: 0; top: 0;
  -webkit-transition: none;
  transition: none;
  -webkit-transform: rotateY(10deg) translateZ(-100px) ;
          transform: rotateY(10deg) translateZ(-100px) ;
}

/* 准备一个编辑器 */
.resumeEditor{
  position: fixed; right: 0; top: 0;
  padding: .5em;  margin: .5em;
  width: 48vw; height: 90vh;
  border: 1px solid;
  background: rgb(234,234,239); color: #222;
  overflow: auto;
}
/* 开始写简历 */
`,
        `
/*将Markdown格式翻译成HTML
 *再对HTML加点样式
*/
.resumeEditor{
  padding: 2em;
}
.resumeEditor h2{
  display: inline-block;
  border-bottom: 1px solid;
  margin: 1em 0 .5em;
}
.resumeEditor ul,.resumeEditor ol{
  list-style: none;
}
.resumeEditor ul> li::before{
  content: '•';
  margin-right: .5em;
}
.resumeEditor ol {
  counter-reset: section;
}
.resumeEditor ol li::before {
  counter-increment: section;
  content: counters(section, ".") " ";
  margin-right: .5em;
}
.resumeEditor blockquote {
  margin: 1em;
  padding: .5em;
  background: #ddd;
}
`
      ],
      currentMarkdown: "",
      fullMarkdown: `
     _____    _    _    ____    ______   __   _   _______  __     _
    |  _  \\  | |  | |  / __ \\  |  ____| |  \\ | | |__   __| \\ \\   / /
    | |_|  | | |__| | | |  | | | |____  |   \\| |    | |     \\ \\_/ /
    |  ___/  |  __  | | |  | | |  ____| | |\\ | |    | |      | _ |
    | |      | |  | | | |__| | | |____  | | \\  |  __| |__   / / \\ \\
    |_|      |_|  |_|  \\____/  |______| |_|  \\_| |_______| /_/   \\_\\
<br>


个人简历
----
你好，我是 Phoenix，一名软件研发人员，目前坐标广东广州。
熟练掌握 C++、go 等编程语言，基本功扎实。有着良好的文档编写能力及编码习惯
英文能力良好，能熟练阅读及编写英文资料及文档
热衷技术，追求理性，能独立解决技术问题，百折不挠

技能
----
* 后端开发
* 网络编程
* 分布式
* 数据结构与算法
* Linux
* 开源爱好者
* 博客系统
* 英语

技术及语言
----
  - **语言**: 熟悉 C++、Go语言开发，了解 lua、 python 语言，具备一定的脚本能力
  - **数据库**: MySQL、redis
  - **网络库**: muduo、libevent
  - **OS**: Linux、Windows
  - **Others**: Git、Google Protobuf、Google Test Framework、cmake、clang、gdb、valgrind、conan

工作经历
----
在广州飞歌汽车音响有限公司后装技术部担任嵌入式系统工程师，负责车载导航系统的驱动开发以及系统研发

开源项目
----
**C++ 项目**:
> 1. [基于 http 协议实现的 web 服务器 TinyWebServer](https://github.com/Phoenix500526/TinyWebServer.git)
> 2. [基于 Reactor 模式实现的网络库 Tmuduo](https://github.com/Phoenix500526/Tmuduo.git)
> 3. [基于 DFA 实现的正则表达式引擎 T-Reg](https://github.com/Phoenix500526/T-Reg.git)

**Golang 项目**:
> 1. [简易版分布式缓存系统 go-cache](https://github.com/Phoenix500526/go-cache.git)
> 2. [简易版 web 框架 go-web](https://github.com/Phoenix500526/go-web)

**Other**
> 1. [基于 Hexo 框架实现的个人技术网站 —— Hacker-cube](https://www.hacker-cube.com)

链接
----
* [技术博客 —— hacker-cube](https://www.hacker-cube.com/)
* [GitHub](https://github.com/Phoenix500526)
* [StackOverflow](https://stackoverflow.com/users/8557622/phoenix-chao?tab=profile)
* [简书](https://www.jianshu.com/u/d2aa8a7f1468)
* [leetcode](https://leetcode-cn.com/u/jin-ji-de-lancelot/)

归档文章
----
* [muduo源码剖析](https://www.hacker-cube.com/categories/muduo%E6%BA%90%E7%A0%81%E5%89%96%E6%9E%90//)
* [skynet源码剖析](https://www.hacker-cube.com/categories/skynet%E6%BA%90%E7%A0%81%E5%89%96%E6%9E%90//)
* [研发专用瑞士军刀](https://www.hacker-cube.com/categories/%E7%91%9E%E5%A3%AB%E5%86%9B%E5%88%80//)
* [学而时嬉之](https://www.hacker-cube.com/categories/%E5%AD%A6%E8%80%8C%E6%97%B6%E5%AC%89%E4%B9%8B/)


联系我
----
* 联系方式：
> QQ：**519788069** 
> 微信：**Phoenix500526** 
> 邮箱：[163邮箱](mailto:phoenix500526@163.com)|[gmail邮箱](mailto:Phoenix400426@gmail.com)
* 主要涉及技术：**C++后端开发**、**C++网络编程**、**Go语言**、**lua语言**、**开源爱好者**、**Linux**

> 如果你喜欢这个简历效果，欢迎 fork [我的简历](git@github.com:Phoenix500526/Animation-Resume.git), 打造属于自己的动态简历
`
    };
  },
  created() {
    this.makeResume();
  },

  methods: {
    makeResume: async function() {
      await this.progressivelyShowStyle(0);
      await this.progressivelyShowResume();
      await this.progressivelyShowStyle(1);
      await this.showHtml();
      await this.progressivelyShowStyle(2);
    },
    showHtml() {
      return new Promise((resolve, reject) => {
        this.enableHtml = true;
        resolve();
      });
    },
    progressivelyShowStyle(n) {
      return new Promise((resolve, reject) => {
        let interval = this.interval;
        let showStyle = async function() {
          let style = this.fullStyle[n];
          if (!style) {
            return;
          }
          // 计算前 n 个 style 的字符总数
          let length = this.fullStyle
            .filter((_, index) => index <= n)
            .map(item => item.length)
            .reduce((p, c) => p + c, 0);
          let prefixLength = length - style.length;
          if (this.currentStyle.length < length) {
            let l = this.currentStyle.length - prefixLength;
            let char = style.substring(l, l + 1) || " ";
            this.currentStyle += char;
            if (style.substring(l - 1, l) === "\n" && this.$refs.styleEditor) {
              this.$nextTick(() => {
                this.$refs.styleEditor.goBottom();
              });
            }
            setTimeout(showStyle, interval);
          } else {
            resolve();
          }
        }.bind(this);
        showStyle();
      });
    },
    progressivelyShowResume() {
      return new Promise((resolve, reject) => {
        let length = this.fullMarkdown.length;
        let interval = this.interval;
        let showResume = () => {
          if (this.currentMarkdown.length < length) {
            this.currentMarkdown = this.fullMarkdown.substring(
              0,
              this.currentMarkdown.length + 1
            );
            let lastChar = this.currentMarkdown[
              this.currentMarkdown.length - 1
            ];
            let prevChar = this.currentMarkdown[
              this.currentMarkdown.length - 2
            ];
            if (prevChar === "\n" && this.$refs.resumeEditor) {
              this.$nextTick(() => this.$refs.resumeEditor.goBottom());
            }
            setTimeout(showResume, interval);
          } else {
            resolve();
          }
        };
        showResume();
      });
    }
  }
};
</script>

<style scoped>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

html {
  min-height: 100vh;
}

* {
  box-sizing: border-box;
}
</style>
