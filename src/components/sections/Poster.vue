<script setup>
const props = defineProps({
  src: { type: String, required: true },
  alt: { type: String, default: 'Poster' }
})
</script>

<template>
  <div>
    <el-divider />

    <el-row justify="center" id="exPoster">
      <h1 class="section-title">Poster</h1>
    </el-row>

    <el-row justify="center">
      <el-col :span="20">
        <div class="poster">
          <img :src="props.src" :alt="props.alt" />
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<style scoped>
.poster{ text-align:center; margin:1px 0; }
.poster img{ width:90%; max-width:100%; height:auto; display:inline-block; }
.section-title{ font-size:28px; text-align:center; margin:1px 0; }
</style>
