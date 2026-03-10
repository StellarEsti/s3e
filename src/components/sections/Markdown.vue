<script setup>
import page from '../mds/md.mdx';
</script>

<template>
  <div>
    <el-divider />

    <el-row justify="center">
        <el-col :xs="24" :sm="20" :md="16" :lg="12" :xl="12">
        <page />
        </el-col>
    </el-row>

  </div>
</template>

<style scoped>
:deep(h1),
:deep(h2),
:deep(h3),
:deep(h4),
:deep(h5),
:deep(h6) {
  font-family: Arial, "Helvetica Neue", Helvetica, sans-serif;
}
</style>