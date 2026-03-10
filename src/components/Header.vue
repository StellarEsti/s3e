<script lang="ts" setup>

import { ElIcon } from 'element-plus'
import { HomeFilled, SuccessFilled } from '@element-plus/icons-vue'
import { inject } from 'vue'

// 个人主页
const home = {
    name: "My Blog",
    link: "https://junyaohu.github.io/",
}

// 项目主页
const logo = {
    name: "Template",
    link: "#",
}

// 右侧更多菜单
const more_paper = {
    "ExtDM": {
        name: "ExtDM - CVPR 2024",
        link: "https://zzcheng.top/ExtDM/",
    },
    "MPOT": {
        name: "MPOT - ICCV 2023",
        link: "https://zzcheng.top/MPOT/",
    },
    "ControlNet": {
        name: "ControlNet - ICCV 2023",
        link: "https://github.com/lllyasviel/ControlNet",
    }
}

const theme = inject('theme')
const toggleTheme = inject('toggleTheme')

function onToggle() {
  if (typeof toggleTheme === 'function') toggleTheme()
}

</script>

<template>
    <!-- 设置页首始终悬浮顶部 -->
    <el-affix :offset="0" :style="{width: '100%'}">
    
    <!-- 水平导航目录 -->
    <el-menu 
        default-active="1"
        class="el-menu-demo"
        mode="horizontal"
        :ellipsis="false"
    >
        <!-- 个人主页 -->
        <el-menu-item index="0" >
            <el-icon :size="20"><HomeFilled /></el-icon>
            <a :href=home.link>{{ home.name }} </a>
        </el-menu-item>
        
        <!-- 项目主页 -->
        <el-menu-item index="1">
            <el-icon :size="20"><SuccessFilled /></el-icon>
            <a :href=logo.link>{{ logo.name }} </a>
        </el-menu-item>

        <!-- 更多栏目 -->
        <el-sub-menu index="2">
            <template #title>More</template>
            <el-menu-item index="2-1">
                <a :href=more_paper.ExtDM.link>{{ more_paper.ExtDM.name }}</a>
            </el-menu-item>
            <el-menu-item index="2-2">
                <a :href=more_paper.MPOT.link>{{ more_paper.MPOT.name }}</a>
            </el-menu-item>
            <el-menu-item index="2-3">
                <a :href=more_paper.ControlNet.link>{{ more_paper.ControlNet.name }}</a>
            </el-menu-item>
        </el-sub-menu>

        <!-- 主题切换器 -->
        <el-menu-item index="theme-toggle" class="theme-toggle-item" @click="onToggle">
            <div class="theme-toggle" :class="theme">
                <div class="toggle-track">
                    <div class="knob">{{ theme === 'dark' ? '🌙' : '☀️' }}</div>
                </div>
            </div>
        </el-menu-item>
    </el-menu>
    </el-affix>
</template>

<style>

/* 导航背景 */
.el-menu {
	background: none;
}

/* 下拉菜单宽度 */
.el-menu--popup {
	min-width: 100%;
}

/* 导航背景特效和阴影 */
.el-affix--fixed {
	box-shadow: 1px 1px 2px rgba(0, 0, 0, 0.1);
	background-image: radial-gradient(#ffffffca 1px,#ffffff 1px);
	background-size: 3px 3px;
}

/* 水平导航高度 */
.el-header {
    --el-header-height: 50px;
}

</style>

<style scoped>

/* 水平导航左右分区 */
.el-menu--horizontal > .el-menu-item:nth-child(2) {
    margin-right: auto;
}

/* 水平导航高度 */
.el-menu--horizontal {
    --el-menu-horizontal-height: 50px;
}

/* 把主题切换器推到右侧 */
.el-menu--horizontal > .theme-toggle-item {
    margin-left: auto;
}

/* 取消鼠标焦点悬浮在链接上的颜色装饰 */
a:hover {
  color: inherit;
  border-bottom: none;
}

/* 链接装饰，取消下划线和链接颜色 */
a {
	text-decoration: None;
	color: inherit;
}

/* 胶囊切换器样式 */
.theme-toggle-item {
    cursor: pointer;
    padding: 10px 16px;
}
.theme-toggle {
    display: inline-flex;
    align-items: center;
}
.theme-toggle .toggle-track {
    width: 46px;
    height: 24px;
    border-radius: 999px;
    background: rgba(0,0,0,0.08);
    position: relative;
    transition: background .2s ease;
}
.theme-toggle .knob {
    width: 20px;
    height: 20px;
    border-radius: 999px;
    background: #fff;
    position: absolute;
    top: 2px;
    left: 2px;
    box-shadow: 0 1px 3px rgba(0,0,0,0.2);
    transition: left .18s ease, background .18s ease, transform .18s ease;
}
.theme-toggle .knob {
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 12px;
}
.theme-toggle.dark .toggle-track {
    background: rgba(255,255,255,0.12);
}
.theme-toggle.dark .knob {
    left: 24px;
    background: #fff;
}

</style>

  