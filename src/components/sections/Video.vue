<script setup>
import { ref, onMounted } from 'vue'

const base = import.meta.env.BASE_URL
const videos = [
  { src: `${base}/public/video/Camera.mp4`, title: 'Scene', badge: 'Camera' },
  { src: `${base}/public/video/EKF-RIO.mp4`, title: 'EKF-RIO', badge: 'Point-based RIO' },
  { src: `${base}/public/video/PG-RIO.mp4`, title: 'PG-RIO', badge: 'Point-based RIO' },
  { src: `${base}/public/video/4D-RIO.mp4`, title: '4D-RIO', badge: 'Point-based RIO' },
  { src: `${base}/public/video/Ours.mp4`, title: 'Ours', badge: 'Spectra-Based RIO' },
  { src: `${base}/public/video/LiDAR_SLAM.mp4`, title: 'LiDAR Odometry', badge: 'LIO' },
]

const selectedIdx = ref(Math.max(0, videos.findIndex(v => v.title === 'Ours')))
function select(idx) { selectedIdx.value = idx }

onMounted(() => {
  // enable autoplay for muted videos; call play() to start playback
  const vids = document.querySelectorAll('.video-box video')
  vids.forEach((v) => {
    try {
      v.autoplay = true
      v.muted = true
      // browsers may reject play() if not allowed; ignore errors
      v.play().catch(() => {})
    } catch (e) {}
  })
})
</script>

<template>
  <div>
    <el-divider />

    <el-row justify="center">
      <h1 class="section-title" id="exVideo">Demo Video</h1>
    </el-row>

    <!-- 每个网站的视频的iframe可能不一致，最好在这里手动调整 -->
    <el-row justify="center">
      <el-col :span="24">
        <div class="video-grid-wrapper">
          <el-row :gutter="20" class="video-grid" justify="center">
            <el-col :xs="24" :sm="12" :md="8" v-for="(video, idx) in videos" :key="idx">
              <div class="video-box" :class="{ selected: selectedIdx === idx }" @click="select(idx)">
                <div class="video-topbar">
                  <div class="topbar-title">{{ video.title }}</div>
                  <div class="topbar-badge" v-if="video.badge">{{ video.badge }}</div>
                </div>
                <div class="video-inner">
                  <video controls muted preload playsinline>
                    <source :src="video.src" type="video/mp4" />
                  </video>
                </div>
                <div class="selected-pill" v-if="selectedIdx === idx">SELECTED</div>
              </div>
            </el-col>
          </el-row>
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<style scoped>

.video-grid-wrapper{
  width: 90%;
  margin: 0 auto 12px auto;
}

.video-grid .el-col {
  margin-bottom: 14px; /* vertical gap between rows */
}

.video-box{
  /* outer frame (light theme: white frame like reference) */
  background: var(--frame-bg, #282626);
  border-radius: 12px;
  padding: 0px;
  box-shadow: 0 6px 18px rgba(0,0,0,0.06);
  overflow: visible;
  position: relative;
}

/* inner dark panel that actually holds the video */
.video-inner{
  background: var(--card-bg, #0b0b0b);
  border-radius: 0 0 8px 8px;
  overflow: hidden;
}

.video-inner video{
  aspect-ratio: 16 / 9;
  width: 100%;
  display: block;
  background: #000;
}

.video-topbar{
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 14px;
  background: rgba(51, 51, 51, 0.85);
  color: #fff;
  border-radius: 12px 12px 0 0;
  border-bottom: 1px solid var(--topbar-sep, rgba(255,255,255,0.06));
  font-weight: 700;
  z-index: 3;
}

.video-topbar .topbar-title{
  font-size: 15px;
}

.video-topbar .topbar-badge{
  font-size: 12px;
  background: rgba(255, 255, 255, 0.135);
  color: #960303;
  padding: 4px 8px;
  border-radius: 5px;
}

.video-box .selected-pill{
  position: absolute;
  top: -12px;
  left: 50%;
  transform: translateX(-50%);
  background: #ff9800;
  color: #fff;
  padding: 4px 10px;
  border-radius: 999px;
  font-size: 12px;
  z-index: 4;
  box-shadow: 0 2px 6px rgba(0,0,0,0.2);
}

.video-box.selected{
  box-shadow: 0 0 0 4px rgba(255, 153, 0, 0.382), 0 10px 24px rgba(0,0,0,0.18);
  border: 2px solid rgba(255, 153, 0, 0.618);
}

@media (max-width: 768px) {
  .video-grid-wrapper{ width: 96%; }
  .video-box{ padding: 6px; box-shadow: 0 4px 12px rgba(0,0,0,0.08); }
}

</style>