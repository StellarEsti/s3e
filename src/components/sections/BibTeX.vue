<script>
export default {
  data() {
    return {
      bibtex: [
        "@InProceedings{Wang_2025_ICCV,",
        "    author    = {Wang, Shengpeng and Xie, Yulong and Liao, Qing and Wang, Wei},",
        "    title     = {S3E: Self-Supervised State Estimation for Radar-Inertial System},",
        "    booktitle = {Proceedings of the IEEE/CVF International Conference on Computer Vision (ICCV)},",
        "    month     = {October},",
        "    year      = {2025},",
        "    pages     = {26686-26695}",
        "}"
      ],
    }
  },
  methods: {
    copyVal() {
      let oInput = document.createElement('textarea');
      let text = document.getElementById('bibtex').innerText;
      oInput.value = text;
      document.body.appendChild(oInput);
      oInput.select();
      document.execCommand('Copy');
      this.$message.success('Copy Successfully');
      oInput.remove();
    }
  }
}

</script>

<template>
  <div>
    <el-divider />
      
      <el-row justify="center">
        <h1 class="section-title">BibTeX</h1>
      </el-row>
      
      <el-row justify="center">
        <el-col class='bibtex' :xs="24" :sm="20" :md="14" :lg="12" :xl="12" @click="copyVal()" >
          <div style="text-align: center; color: var(--el-text-color-secondary); margin-top: 20px;">🖱️ Click here to copy BibTex.</div>
          <el-row>
            <el-scrollbar style="margin: 0px 20px 5px 20px;">
              <pre id="bibtex"><code>{{ bibtex.join('\n') }}</code></pre>
            </el-scrollbar>
          </el-row>
        </el-col>
      </el-row>

  </div>
</template>

<style scoped>

.scrollbar-flex-content {
  display: flex;
}

/* 卡片属性 */
.bibtex {
  margin: 20px 0px;
  padding-top: 5px;
  box-shadow: var(--el-box-shadow-light);
  background: var(--card-bg);
  padding-bottom: 12px;
  border-radius: 10px;
}

/* 卡片悬浮 */
.bibtex:hover {
  box-shadow: var(--el-box-shadow); 
}

/* 卡片点击 */
.bibtex:active{
  box-shadow: var(--el-box-shadow-lighter); 
}

pre {
  border: none;
  background: transparent;
  margin: 0;
  padding: 0;
}

pre code {
  font-size: 18px;
  background: var(--code-bg);
  color: var(--text-color);
  display: block;
  padding: 18px;
  border-radius: 10px;
  white-space: pre-wrap; /* wrap long lines */
  word-break: break-word;
}



</style>