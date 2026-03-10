<script setup>
import { ref, provide } from 'vue'
import Main from './components/Main.vue'
import Footer from './components/Footer.vue'

const theme = ref(localStorage.getItem('theme') || 'light')
function toggleTheme() {
  theme.value = theme.value === 'light' ? 'dark' : 'light'
  localStorage.setItem('theme', theme.value)
}

provide('theme', theme)
provide('toggleTheme', toggleTheme)
</script>

<template>
    <div :class="theme">
      
      <el-container>
        <el-main><Main/></el-main>
      </el-container>
      
      <!-- 回到顶部 -->
      <el-backtop :right="40" :bottom="80" />
    </div>
</template>

<style>

/* 全局主题变量 */
.light {
  --bg-odd: #ffffff;
  --bg-even: #f3f4f6;
  --card-bg: #ffffff;
  --topbar-sep: rgba(160, 157, 157, 0.569);
  --code-bg: #f2f2f2;
  --divider-color: rgba(0,0,0,0.08);
  --text-color: #000000;
  --text-color-secondary: #4b5563;
  --el-box-shadow-light: 0 1px 4px rgba(0,0,0,0.08);
  --el-box-shadow: 0 6px 18px rgba(0,0,0,0.12);
  --el-box-shadow-lighter: 0 2px 6px rgba(0,0,0,0.06);
  --media-filter: none;
  font-family: "Heiti SC", "PingFang SC", system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
}

.dark {
  --bg-odd: #222222;
  --bg-even: #404040;
  --card-bg: #2b2b2b;
  --topbar-sep: rgba(255,255,255,0.06);
  --code-bg: #1e1e1e;
  --divider-color: rgba(255,255,255,0.06);
  --text-color: #ffffff;
  --text-color-secondary: #c7c7c7;
  --el-box-shadow-light: 0 1px 4px rgba(0,0,0,0.2);
  --el-box-shadow: 0 6px 18px rgba(0,0,0,0.35);
  --el-box-shadow-lighter: 0 2px 6px rgba(0,0,0,0.25);
  --media-filter: brightness(0.95) contrast(1.02);
  font-family: "Heiti SC", "PingFang SC", system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
}

/* 全局文字颜色 */
body, .light, .dark {
  color: var(--text-color);
  background: transparent;
}

/* 去除节与节之间的外边距，确保背景无缝衔接 */
html, body {
  margin: 0;
  padding: 0;
}
.el-main {
  padding: 0;
}
.el-main > * {
  margin: 0 !important;
  padding: 0 !important;
  /* 建立 BFC，避免子元素 margin 折叠到父元素外部造成白色缝隙 */
  overflow: auto;
}


/* 为 el-main 下的直接子节点交替设置背景色 */
.light .el-main > *:nth-child(odd),
.light .el-main > div:nth-child(odd) {
  background: var(--bg-odd);
}
.light .el-main > *:nth-child(even),
.light .el-main > div:nth-child(even) {
  background: var(--bg-even);
}
.dark .el-main > *:nth-child(odd),
.dark .el-main > div:nth-child(odd) {
  background: var(--bg-odd);
}
.dark .el-main > *:nth-child(even),
.dark .el-main > div:nth-child(even) {
  background: var(--bg-even);
}

/* 媒体、图片适配 */
img, video, canvas, iframe {
  filter: var(--media-filter);
  transition: filter .25s ease, box-shadow .25s ease;
  max-width: 100%;
}

/* 卡片、代码块、引用等使用卡片背景 */
.el-main .section-title,
.el-main .bibtex,
.el-main pre,
.el-main code {
  color: var(--text-color);
}

/* Element Plus 全局覆盖：避免组件默认白色背景/分割导致的白线 */
.el-affix--fixed {
  background-image: none !important;
  background: transparent !important;
  box-shadow: none !important;
}

/* 分隔线颜色按主题调整，避免纯白 */
.el-divider {
  height: 1px;
  border: none !important;
  background: var(--divider-color) !important;
  margin: 0 !important;
  padding: 0 !important;
  display: block;
  position: relative;
  z-index: 20;
}

/* 折叠面板/卡片/滚动容器使用透明背景并使用主题边框 */
.el-collapse,
.el-collapse-item,
.el-collapse-item__header,
.el-collapse-item__content,
.el-card,
.el-card__body,
.el-scrollbar__wrap,
.el-alert,
.el-menu,
.el-menu--horizontal {
  background: transparent !important;
  border-color: transparent !important;
}

/* 折叠项的内边框改为主题适配色，避免白色块 */
.el-collapse-item {
  border-top: 1px solid rgba(0,0,0,0.04);
}
.dark .el-collapse-item {
  border-top-color: rgba(255,255,255,0.04);
}

/* 滚动区域背景透明，代码块等使用卡片背景变量 */
.el-scrollbar__wrap {
  background: transparent !important;
}

/* 进一步覆盖以复刻 ravf-page 风格：
   - 统一把节内居中列设为透明，使用卡片样式展示内容
   - 把折叠、卡片等白色背景替换为主题卡片色，避免白色条纹
*/
.el-main > * {
  padding: 40px 0;
}

/* 保证第一个节与页首无缝 */
.el-main > *:first-child {
  padding-top: 0;
}

/* 中心列透明，卡片样式放在内部容器（.section-card 或 el-card） */
.el-main .el-row > .el-col,
.el-main .el-row,
.el-main .el-col {
  background: transparent !important;
}

/* 卡片统一用主题卡片背景，避免纯白 */
.el-card,
.section-card {
  background: var(--card-bg) !important;
  color: var(--text-color) !important;
  border-radius: 10px;
  box-shadow: var(--el-box-shadow-light) !important;
  padding: 20px;
}

/* 折叠面板改为透明背景，项内容用卡片背景显示 */
.el-collapse,
.el-collapse-item,
.el-collapse-item__header,
.el-collapse-item__content {
  background: transparent !important;
  color: var(--text-color) !important;
}
.el-collapse-item__wrap {
  background: var(--card-bg) !important;
}

/* 按主题调整分割线颜色，避免纯白 */
.el-divider {
  border-color: rgba(0,0,0,0.08) !important;
}
.dark .el-divider {
  border-color: rgba(255,255,255,0.06) !important;
}

/* 警告和滚动条使用透明底 */
.el-alert {
  background: transparent !important;
  border-color: transparent !important;
}

/* 调整标题区域，让背景带满宽度、标题居中且与卡片分离 */
.el-main > * .paper-title,
.el-main > * .section-title {
  padding: 18px 0 12px;
}




h1 {
  font-family: Arial, "Helvetica Neue", Helvetica, sans-serif;
  letter-spacing: 2px;
  font-size: 28px;
  margin: 0px;
  text-align: center;
}

/* 增加 MDX/Markdown 渲染内容中标题与上方分割线的间距
   只作用于页面内容列中的 h1，避免影响 `paper-title` 等特殊标题 */
.el-main .el-row .el-col h1 {
  margin-top: 18px;
}

h2, h3, h4, h5, h6 {
  font-family: Arial, "Helvetica Neue", Helvetica, sans-serif;
  letter-spacing: 2px;
}

.el-header {
  padding: 0px;
}

.el-footer {
  padding: 0px;
}

p, li {
  font-size: 16px;
  line-height: 1.75rem;
}

code {
  font-family: 'Consolas', monospace;
  border-radius: 5px;
  padding: 2px 5px;
  background: #f2f2f2;
  color: black;
}

pre {
  border-radius: 5px;
  padding: 10px;
  background: #f2f2f2;
  line-height: 1.4rem;
}

pre:not(pre[id=bibtex]) {
  overflow-x: auto;
}

pre code {
  font-size: 16px;
  color: black;
  border: none;
  padding: 0px;
}

blockquote {
  border-left: 5px solid #bcbcbc;
  padding: 10px 20px 10px 20px;
  margin: 0px;
  background: #f6f6f6;
}

blockquote > p {
  margin-block-start: 0.5em;
  margin-block-end: 0.5em;
}

/* 链接颜色装饰 */
a {
  color: #3273dc;
  text-decoration: none;
}

/* 鼠标焦点悬浮在链接上的颜色装饰 */
a:hover {
  color: #848484;
  border-bottom: dotted;
}

p > img {
  width: 80%;
  display: block;
  margin: 0 auto;
  border-radius: 10px;
  box-shadow: 1px 1px 4px 1px #afafaf;
}

table {
  border-collapse: collapse;
  width: max-content;
  max-width: 100%;
  margin: 0 auto;
  display:block;
  overflow-x:auto;
}

thead {
  border-bottom-width: 1px;
  border-top-width: 2px;
  border-left-width: 0px;
  border-right-width: 0px;
  border-style: solid;
  border-color: rgb(0 0 0);
}

tbody tr:last-child {
  border-bottom-width: 2px;
  border-top-width: 0px;
  border-left-width: 0px;
  border-right-width: 0px;
  border-style: solid;
  border-color: rgb(0 0 0);
}

th, td {
    padding-left: 1rem;
    padding-right: 1rem;
}

.katex-display {
  overflow-x: auto;
  overflow-y: hidden;
}

</style>