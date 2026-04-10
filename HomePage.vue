<template>
  <div class="home-page">
    <!-- 粒子背景 -->
    <div class="bg-particles" id="homeParticles"></div>
    <div class="bg-orb bg-orb-1"></div>
    <div class="bg-orb bg-orb-2"></div>

    <!-- HERO 区 -->
    <section class="hero-section">
      <div class="hero-content">
        <div class="hero-text">
          <div class="hero-badge">
            <div class="live-dot"></div>
            第12期招生中 · 剩余 18 名额
          </div>
          <h1>
            成为<br>
            <span class="highlight">顶级主播</span><br>
            从这里开始
          </h1>
          <p class="hero-desc">
            专注娱乐直播培训，涵盖个播、团播、带货全场景。
            行业 TOP 导师亲授，真实直播间实操，帮你从素人变网红。
          </p>
          <div class="hero-buttons">
            <el-button type="primary" size="large" @click="router.push('/tutorials')" class="btn-primary">
              🎯 探索课程
            </el-button>
            <el-button size="large" @click="scrollToTracks" class="btn-secondary">
              了解更多 →
            </el-button>
          </div>
          <div class="hero-stats">
            <div class="stat-item">
              <div class="stat-number">8000+</div>
              <div class="stat-label">毕业学员</div>
            </div>
            <div class="stat-item">
              <div class="stat-number">Top 5%</div>
              <div class="stat-label">薪资涨幅</div>
            </div>
            <div class="stat-item">
              <div class="stat-number">96%</div>
              <div class="stat-label">好评率</div>
            </div>
          </div>
        </div>

        <div class="hero-visual">
          <div class="streamer-card">
            <div class="streamer-header">
              <div class="avatar-ring">
                <div class="avatar-inner">🎤</div>
              </div>
              <div class="avatar-vip">⭐</div>
              <div class="streamer-info">
                <h3>学员真实案例</h3>
                <div class="streamer-tags">
                  <span class="tag purple">个播</span>
                  <span class="tag pink">团播</span>
                  <span class="tag gold">带货</span>
                </div>
              </div>
            </div>
            <div class="income-card">
              <div class="income-header">
                <span class="income-title">上月直播收入</span>
                <span class="income-badge">↑ 67%</span>
              </div>
              <div class="income-amount">¥128,400</div>
              <div class="income-compare">较培训前增长 3.2 倍</div>
            </div>
            <div class="platforms">
              <div class="platform-btn active">🎵 抖音</div>
              <div class="platform-btn">📺 快手</div>
              <div class="platform-btn">📱 视频号</div>
            </div>
            <el-button type="primary" class="streamer-cta" @click="router.push('/register')">
              立即报名 →
            </el-button>
          </div>

          <div class="float-card top-right">
            <span class="float-icon">🔥</span>
            <span>学员首月破万</span>
          </div>
          <div class="float-card bottom-left">
            <span class="float-icon">🏆</span>
            <span>导师百万粉账号</span>
          </div>
        </div>
      </div>
    </section>

    <!-- 三大课程 -->
    <section class="tracks-section" id="tracks">
      <div class="section-header">
        <div class="section-label">🎓 三大课程体系</div>
        <h2 class="section-title">找到属于你的赛道</h2>
        <p class="section-desc">无论你想做娱乐主播、团队主播还是带货达人，我们都有专属路径</p>
      </div>

      <div class="track-grid">
        <div class="track-card fade-up" v-for="track in tracks" :key="track.id">
          <div class="track-cover" :style="{ background: track.gradient }">
            <span class="track-emoji">{{ track.emoji }}</span>
            <span class="track-badge" :style="{ background: track.badgeColor }">{{ track.badge }}</span>
          </div>
          <div class="track-content">
            <div class="track-type" :style="{ color: track.color }">{{ track.typeLabel }}</div>
            <h3 class="track-title">{{ track.title }}</h3>
            <p class="track-desc">{{ track.desc }}</p>
            <ul class="track-features">
              <li v-for="f in track.features" :key="f">{{ f }}</li>
            </ul>
            <div class="track-footer">
              <div class="track-price">{{ track.price }} <span>/ {{ track.duration }}</span></div>
              <el-button @click="router.push('/tutorials')" class="track-btn">了解详情</el-button>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- 为什么选择 -->
    <section class="why-section">
      <div class="section-header">
        <div class="section-label">✨ 为什么选择星耀</div>
        <h2 class="section-title">专业，是我们的底线</h2>
      </div>
      <div class="why-grid">
        <div class="why-card fade-up" v-for="w in whyItems" :key="w.title">
          <div class="why-icon" :style="{ background: w.gradient }">{{ w.icon }}</div>
          <h3>{{ w.title }}</h3>
          <p>{{ w.desc }}</p>
        </div>
      </div>
    </section>

    <!-- 热门教程 -->
    <section class="popular-section">
      <div class="section-header row">
        <div>
          <div class="section-label">🔥 热门教程</div>
          <h2 class="section-title">最受学员欢迎的直播秘籍</h2>
        </div>
        <el-button text @click="router.push('/tutorials')" class="view-all">
          查看全部 →
        </el-button>
      </div>

      <div class="tutorial-tabs">
        <div
          v-for="tab in tabs"
          :key="tab.id"
          :class="['tab-item', { active: activeTab === tab.id }]"
          @click="activeTab = tab.id"
        >
          <span>{{ tab.icon }}</span>
          <span>{{ tab.name }}</span>
        </div>
      </div>

      <div class="tutorial-grid">
        <div
          v-for="tutorial in filteredTutorials"
          :key="tutorial.id"
          class="tutorial-card fade-up"
          @click="router.push(`/tutorial/${tutorial.id}`)"
        >
          <div class="tutorial-image" :style="{ background: tutorial.bg }">
            <span class="tutorial-emoji">{{ tutorial.emoji }}</span>
            <span class="difficulty-badge" :class="'level-' + tutorial.difficulty">
              {{ ['入门', '简单', '中等', '进阶', '专家'][tutorial.difficulty - 1] }}
            </span>
            <span v-if="tutorial.is_free" class="free-badge">免费</span>
          </div>
          <div class="tutorial-content">
            <h3 class="tutorial-title">{{ tutorial.title }}</h3>
            <p class="tutorial-desc">{{ tutorial.description }}</p>
            <div class="tutorial-meta">
              <span>⏱️ {{ tutorial.estimated_time }}分钟</span>
              <span>👁️ {{ tutorial.views }}人学</span>
              <span>⭐ {{ tutorial.rating }}</span>
            </div>
            <div class="tutorial-author">
              <span class="author-avatar">{{ tutorial.author_name[0] }}</span>
              <span class="author-name">{{ tutorial.author_name }}</span>
              <span class="author-tag">金牌导师</span>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- 学员故事 -->
    <section class="stories-section">
      <div class="section-header">
        <div class="section-label">🌟 明星学员</div>
        <h2 class="section-title">他们从这里出发</h2>
      </div>
      <div class="stories-grid">
        <div class="story-card fade-up" v-for="s in stories" :key="s.name">
          <div class="story-header">
            <div class="story-avatar">{{ s.avatar }}</div>
            <div>
              <div class="story-name">{{ s.name }}</div>
              <div class="story-role">{{ s.role }}</div>
            </div>
          </div>
          <p class="story-text">"{{ s.text }}"</p>
          <div class="story-stats">
            <div class="story-stat" v-for="stat in s.stats" :key="stat.label">
              <div class="stat-value">{{ stat.value }}</div>
              <div class="stat-label">{{ stat.label }}</div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- CTA -->
    <section class="cta-section">
      <div class="cta-box">
        <h2>准备好<span class="highlight">闪耀</span>了吗？</h2>
        <p>第12期招生中。扫码咨询，领取免费试听课和直播资料包。</p>
        <div class="cta-buttons">
          <el-button type="primary" size="large" @click="router.push('/register')" class="btn-primary">
            📩 立即咨询
          </el-button>
          <el-button size="large" @click="router.push('/tutorials')" class="btn-secondary">
            看课程详情 →
          </el-button>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'
import { useRouter } from 'vue-router'
import { ElMessage } from 'element-plus'

const router = useRouter()

const tabs = [
  { id: 'all', name: '全部热门', icon: '🔥' },
  { id: 'new', name: '最新发布', icon: '🆕' },
  { id: 'rising', name: '急速上升', icon: '📈' },
  { id: 'free', name: '免费精选', icon: '🎁' },
]
const activeTab = ref('all')

const tracks = [
  {
    id: 1,
    emoji: '🎤',
    typeLabel: '🎙️ 个人直播',
    title: '魅力主播养成班',
    desc: '从0粉丝到万人在线，系统的个人IP打造课程。',
    features: ['个人定位与人设设计', '直播间互动技巧', '粉丝维护与变现', '抖音/快手算法揭秘'],
    price: '¥2999',
    duration: '15天',
    gradient: 'linear-gradient(135deg, #A855F7, #7C3AED)',
    badge: '最热门',
    badgeColor: '#A855F7',
    color: '#C084FC',
  },
  {
    id: 2,
    emoji: '👥',
    typeLabel: '🎭 团播公会',
    title: '团播公会创业班',
    desc: '组建自己的主播团队，公会运营与管理的全链路。',
    features: ['公会搭建与招募', '团播内容策划', '运营团队管理', '平台政策与分成'],
    price: '¥5999',
    duration: '30天',
    gradient: 'linear-gradient(135deg, #EC4899, #DB2777)',
    badge: '新趋势',
    badgeColor: '#EC4899',
    color: '#F472B6',
  },
  {
    id: 3,
    emoji: '🛒',
    typeLabel: '💰 直播带货',
    title: '带货主播进阶营',
    desc: '从选品到售后，全流程带货技能，帮你实现睡后收入。',
    features: ['选品与供应链', '直播间话术设计', '流量投放技巧', '数据复盘优化'],
    price: '¥4999',
    duration: '20天',
    gradient: 'linear-gradient(135deg, #F472B6, #FBBF24)',
    badge: '高收入',
    badgeColor: '#F59E0B',
    color: '#FCD34D',
  },
]

const whyItems = [
  { icon: '🎓', title: '体系化教学', desc: '自创「星耀直播法」，科学拆解直播各环节，零基础也能听懂', gradient: 'linear-gradient(135deg, #A855F7, #7C3AED)' },
  { icon: '👨‍🏫', title: '头部导师', desc: '导师均为百万粉丝账号操盘手，真实经验倾囊相授', gradient: 'linear-gradient(135deg, #EC4899, #F472B6)' },
  { icon: '🎥', title: '真实直播间', desc: '1:1还原真实直播间场景，实操比例占70%，学的就是实战', gradient: 'linear-gradient(135deg, #F472B6, #FBBF24)' },
  { icon: '🤝', title: '全程陪跑', desc: '毕业后仍持续答疑，账号诊断服务，终身社群资源对接', gradient: 'linear-gradient(135deg, #FBBF24, #F59E0B)' },
]

const tutorials = ref([
  { id: 1, title: '直播间场景布置终极指南', description: '从零打造专业直播间，让你的画面秒杀99%主播', emoji: '🎬', difficulty: 2, estimated_time: 60, views: 12543, rating: 4.8, is_free: true, bg: 'linear-gradient(135deg, #667eea, #764ba2)', author_name: '场景设计大师', tags: ['场景', '灯光'] },
  { id: 2, title: '美颜参数精细调节秘籍', description: '告别网红脸，打造自然又上镜的直播美颜参数', emoji: '✨', difficulty: 3, estimated_time: 45, views: 23456, rating: 4.9, is_free: true, bg: 'linear-gradient(135deg, #f093fb, #f5576c)', author_name: '美颜研究员', tags: ['美颜', '参数'] },
  { id: 3, title: '电商直播转化率翻倍技巧', description: '单场直播GMV提升300%的秘密武器', emoji: '💰', difficulty: 4, estimated_time: 90, views: 18976, rating: 4.7, is_free: false, bg: 'linear-gradient(135deg, #4facfe, #00f2fe)', author_name: '带货王导师', tags: ['电商', '转化'] },
  { id: 4, title: '话术技巧：让观众忍不住下单', description: '经典话术拆解，让你的转化率提升10倍', emoji: '🗣️', difficulty: 3, estimated_time: 50, views: 30124, rating: 4.9, is_free: false, bg: 'linear-gradient(135deg, #fa709a, #fee140)', author_name: '话术女王', tags: ['话术', '转化'] },
  { id: 5, title: '团播公会从0到1搭建指南', description: '手把手教你建立自己的直播帝国', emoji: '🏢', difficulty: 5, estimated_time: 120, views: 8765, rating: 4.6, is_free: false, bg: 'linear-gradient(135deg, #a18cd1, #fbc2eb)', author_name: '公会创始人', tags: ['公会', '运营'] },
  { id: 6, title: '抖音算法深度解析', description: '摸透平台推荐机制，让流量翻10倍', emoji: '🔢', difficulty: 4, estimated_time: 80, views: 45678, rating: 4.8, is_free: true, bg: 'linear-gradient(135deg, #2af598, #009efd)', author_name: '流量大师', tags: ['算法', '流量'] },
])

const filteredTutorials = computed(() => {
  let list = [...tutorials.value]
  if (activeTab.value === 'new') list.sort((a, b) => b.id - a.id)
  else if (activeTab.value === 'rising') list.sort((a, b) => b.views - a.views)
  else if (activeTab.value === 'free') list = list.filter(t => t.is_free)
  return list
})

const stories = [
  { avatar: '👩', name: '小雨', role: '娱乐主播 · 抖音 28万粉', text: '以前就是个普通上班族，学完个播课后第二周就破了十万在线。现在副业收入已经是主业的2倍了，真的改变了我的人生轨迹。', stats: [{ value: '2000+', label: '场均在线' }, { value: '10倍', label: '收入增长' }] },
  { avatar: '👨', name: '阿杰', role: '公会创始人 · 快手合作', text: '团播课帮我打开了新思路，三个月组建了15人公会，月流水破百万。导师教的不只是技术，更是这个行业真正的玩法。', stats: [{ value: '15人', label: '团队规模' }, { value: '100万+', label: '月流水' }] },
  { avatar: '👩', name: '小雪', role: '带货主播 · 月GMV 80万', text: '带货课最大的收获是学会了数据思维。以前靠运气，现在靠方法论。选品和话术这两块内容价值百万，感谢星耀！', stats: [{ value: '80万', label: '月GMV' }, { value: '300%', label: '转化提升' }] },
]

const scrollToTracks = () => {
  document.getElementById('tracks')?.scrollIntoView({ behavior: 'smooth' })
}

onMounted(() => {
  // 粒子动画
  const container = document.getElementById('homeParticles')
  if (container) {
    for (let i = 0; i < 25; i++) {
      const p = document.createElement('div')
      p.className = 'particle'
      p.style.left = Math.random() * 100 + '%'
      p.style.animationDelay = Math.random() * 15 + 's'
      p.style.animationDuration = (15 + Math.random() * 10) + 's'
      container.appendChild(p)
    }
  }

  // 滚动动画
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) entry.target.classList.add('visible')
    })
  }, { threshold: 0.1 })
  document.querySelectorAll('.fade-up').forEach(el => observer.observe(el))
})
</script>

<style scoped>
.home-page {
  background: #07050D;
  color: #fff;
  min-height: 100vh;
  position: relative;
  overflow-x: hidden;
}

/* 粒子背景 */
.bg-particles {
  position: fixed;
  inset: 0;
  pointer-events: none;
  z-index: 0;
  overflow: hidden;
}

.particle {
  position: absolute;
  width: 3px;
  height: 3px;
  background: #C084FC;
  border-radius: 50%;
  opacity: 0.2;
  animation: rise 18s infinite;
}

@keyframes rise {
  0% { transform: translateY(100vh) scale(0); opacity: 0; }
  10% { opacity: 0.2; }
  90% { opacity: 0.2; }
  100% { transform: translateY(-10vh) scale(1); opacity: 0; }
}

.bg-orb {
  position: fixed;
  border-radius: 50%;
  filter: blur(120px);
  opacity: 0.08;
  pointer-events: none;
  z-index: 0;
}

.bg-orb-1 {
  width: 700px;
  height: 700px;
  background: #A855F7;
  top: -200px;
  right: -200px;
}

.bg-orb-2 {
  width: 500px;
  height: 500px;
  background: #EC4899;
  bottom: -100px;
  left: -100px;
}

section {
  position: relative;
  z-index: 1;
}

/* ===== HERO ===== */
.hero-section {
  min-height: 100vh;
  display: flex;
  align-items: center;
  padding: 120px 0 80px;
}

.hero-content {
  max-width: 1300px;
  margin: 0 auto;
  padding: 0 40px;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 80px;
  align-items: center;
}

.hero-badge {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  padding: 10px 18px;
  background: rgba(168, 85, 247, 0.15);
  border: 1px solid rgba(168, 85, 247, 0.3);
  border-radius: 50px;
  font-size: 0.85rem;
  font-weight: 600;
  color: #C084FC;
  margin-bottom: 28px;
}

.live-dot {
  width: 8px;
  height: 8px;
  background: #EF4444;
  border-radius: 50%;
  animation: pulse 1.5s ease-in-out infinite;
}

@keyframes pulse {
  0%, 100% { opacity: 1; transform: scale(1); }
  50% { opacity: 0.4; transform: scale(1.4); }
}

.hero-text h1 {
  font-size: clamp(2.8rem, 6vw, 4.5rem);
  font-weight: 900;
  line-height: 1.05;
  margin-bottom: 24px;
  letter-spacing: -1px;
}

.highlight {
  background: linear-gradient(135deg, #A855F7, #EC4899);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.hero-desc {
  font-size: 1.15rem;
  color: #94a3b8;
  margin-bottom: 40px;
  max-width: 520px;
  line-height: 1.8;
}

.hero-buttons { display: flex; gap: 16px; flex-wrap: wrap; margin-bottom: 60px; }

.btn-primary {
  background: linear-gradient(135deg, #A855F7, #EC4899) !important;
  border: none !important;
  padding: 16px 36px !important;
  font-size: 1rem !important;
  font-weight: 700 !important;
  border-radius: 60px !important;
  box-shadow: 0 0 60px rgba(168, 85, 247, 0.4);
  transition: all 0.3s;
  color: #fff !important;
}

.btn-primary:hover {
  transform: translateY(-3px);
  box-shadow: 0 0 80px rgba(168, 85, 247, 0.6);
}

.btn-secondary {
  background: rgba(255,255,255,0.06) !important;
  border: 1px solid rgba(255,255,255,0.1) !important;
  color: #fff !important;
  padding: 16px 36px !important;
  font-size: 1rem !important;
  font-weight: 600 !important;
  border-radius: 60px !important;
  transition: all 0.3s;
}

.btn-secondary:hover {
  background: rgba(168,85,247,0.15) !important;
  border-color: #A855F7 !important;
}

.hero-stats {
  display: flex;
  gap: 48px;
  padding-top: 40px;
  border-top: 1px solid rgba(255,255,255,0.08);
}

.stat-item { text-align: left; }

.stat-number {
  font-size: 2.5rem;
  font-weight: 900;
  background: linear-gradient(135deg, #A855F7, #EC4899);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.stat-label {
  font-size: 0.85rem;
  color: #64748b;
  margin-top: 4px;
}

/* 右侧卡片 */
.hero-visual { position: relative; }

.streamer-card {
  background: rgba(168, 85, 247, 0.08);
  backdrop-filter: blur(24px);
  border: 1px solid rgba(255,255,255,0.08);
  border-radius: 24px;
  padding: 28px;
  position: relative;
  overflow: hidden;
}

.streamer-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 4px;
  background: linear-gradient(90deg, #A855F7, #EC4899);
}

.streamer-header {
  display: flex;
  align-items: center;
  gap: 16px;
  margin-bottom: 24px;
}

.avatar-ring {
  width: 72px;
  height: 72px;
  border-radius: 20px;
  background: linear-gradient(135deg, #A855F7, #EC4899);
  padding: 3px;
  animation: ring-pulse 3s ease-in-out infinite;
}

@keyframes ring-pulse {
  0%, 100% { box-shadow: 0 0 0 0 rgba(168,85,247,0.4); }
  50% { box-shadow: 0 0 0 10px rgba(168,85,247,0); }
}

.avatar-inner {
  width: 100%;
  height: 100%;
  border-radius: 17px;
  background: #0F0A1A;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 30px;
}

.avatar-vip {
  position: absolute;
  bottom: 60px;
  left: 70px;
  width: 24px;
  height: 24px;
  background: #FBBF24;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 12px;
  border: 2px solid #07050D;
}

.streamer-info h3 { font-size: 1.2rem; font-weight: 800; margin-bottom: 8px; }

.streamer-tags { display: flex; gap: 6px; flex-wrap: wrap; }

.tag {
  padding: 4px 10px;
  border-radius: 6px;
  font-size: 0.72rem;
  font-weight: 600;
}

.tag.purple { background: rgba(168,85,247,0.2); color: #C084FC; }
.tag.pink { background: rgba(236,72,153,0.2); color: #F472B6; }
.tag.gold { background: rgba(251,191,36,0.2); color: #FBBF24; }

.income-card {
  background: rgba(168,85,247,0.1);
  border: 1px solid rgba(168,85,247,0.2);
  border-radius: 14px;
  padding: 20px;
  margin-bottom: 20px;
}

.income-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 12px;
}

.income-title { font-size: 0.85rem; color: #94a3b8; }

.income-badge {
  padding: 4px 10px;
  background: #FBBF24;
  border-radius: 6px;
  font-size: 0.7rem;
  font-weight: 800;
  color: #07050D;
}

.income-amount {
  font-size: 2.2rem;
  font-weight: 900;
  background: linear-gradient(135deg, #A855F7, #EC4899);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.income-compare { font-size: 0.8rem; color: #22C55E; margin-top: 4px; }

.platforms { display: flex; gap: 10px; margin-bottom: 20px; }

.platform-btn {
  flex: 1;
  padding: 12px;
  background: rgba(255,255,255,0.05);
  border: 1px solid rgba(255,255,255,0.08);
  border-radius: 10px;
  text-align: center;
  font-size: 0.85rem;
  font-weight: 600;
  color: #94a3b8;
  cursor: pointer;
  transition: all 0.3s;
}

.platform-btn:hover, .platform-btn.active {
  background: rgba(168,85,247,0.15);
  border-color: #A855F7;
  color: #C084FC;
}

.streamer-cta {
  width: 100%;
  background: linear-gradient(135deg, #A855F7, #EC4899) !important;
  border: none !important;
  color: #fff !important;
  font-weight: 700 !important;
  padding: 14px !important;
  border-radius: 12px !important;
}

.float-card {
  position: absolute;
  padding: 14px 18px;
  background: #0F0A1A;
  border: 1px solid rgba(255,255,255,0.08);
  border-radius: 14px;
  backdrop-filter: blur(16px);
  display: flex;
  align-items: center;
  gap: 10px;
  font-size: 0.85rem;
  font-weight: 600;
  animation: float-y 4s ease-in-out infinite;
  box-shadow: 0 10px 40px rgba(0,0,0,0.4);
}

.float-card.top-right { top: -20px; right: -30px; animation-delay: 0s; }
.float-card.bottom-left { bottom: -20px; left: -30px; animation-delay: 2s; }

@keyframes float-y {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-12px); }
}

.float-icon { font-size: 1.4rem; }

/* ===== 三大课程 ===== */
.tracks-section {
  padding: 120px 0;
}

.section-header {
  max-width: 1300px;
  margin: 0 auto 60px;
  padding: 0 40px;
  text-align: center;
}

.section-label {
  font-size: 0.85rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 3px;
  background: linear-gradient(135deg, #A855F7, #EC4899);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  margin-bottom: 12px;
}

.section-title {
  font-size: clamp(2rem, 4vw, 3rem);
  font-weight: 900;
  margin-bottom: 16px;
}

.section-desc {
  font-size: 1.1rem;
  color: #94a3b8;
  max-width: 600px;
  margin: 0 auto;
}

.track-grid {
  max-width: 1300px;
  margin: 0 auto;
  padding: 0 40px;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 28px;
}

.track-card {
  background: rgba(168, 85, 247, 0.06);
  border: 1px solid rgba(255,255,255,0.08);
  border-radius: 24px;
  overflow: hidden;
  transition: all 0.4s;
  cursor: pointer;
}

.track-card:hover {
  transform: translateY(-12px);
  border-color: #A855F7;
  box-shadow: 0 30px 80px rgba(168, 85, 247, 0.2);
}

.track-cover {
  height: 200px;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 80px;
}

.track-cover::after {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(to bottom, transparent 30%, rgba(7,5,13,1));
}

.track-badge {
  position: absolute;
  top: 16px;
  right: 16px;
  padding: 8px 16px;
  border-radius: 10px;
  font-size: 0.8rem;
  font-weight: 700;
  z-index: 1;
  color: #fff;
}

.track-content { padding: 28px; }

.track-type {
  font-size: 0.8rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 1px;
  margin-bottom: 12px;
}

.track-title {
  font-size: 1.4rem;
  font-weight: 800;
  margin-bottom: 12px;
}

.track-desc {
  font-size: 0.9rem;
  color: #94a3b8;
  line-height: 1.7;
  margin-bottom: 20px;
}

.track-features {
  list-style: none;
  padding: 0;
  margin: 0 0 24px;
}

.track-features li {
  display: flex;
  align-items: center;
  gap: 10px;
  font-size: 0.85rem;
  color: #94a3b8;
  margin-bottom: 10px;
}

.track-features li::before {
  content: '✓';
  width: 20px;
  height: 20px;
  background: rgba(168,85,247,0.2);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 0.7rem;
  color: #C084FC;
  flex-shrink: 0;
}

.track-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-top: 20px;
  border-top: 1px solid rgba(255,255,255,0.08);
}

.track-price {
  font-size: 1.5rem;
  font-weight: 900;
  color: #C084FC;
}

.track-price span {
  font-size: 0.8rem;
  font-weight: 500;
  color: #64748b;
}

.track-btn {
  background: rgba(255,255,255,0.06) !important;
  border: 1px solid rgba(255,255,255,0.1) !important;
  color: #fff !important;
  padding: 10px 20px !important;
  border-radius: 50px !important;
  font-size: 0.85rem !important;
  font-weight: 600 !important;
  transition: all 0.3s;
}

.track-btn:hover {
  background: linear-gradient(135deg, #A855F7, #EC4899) !important;
  border-color: transparent !important;
}

/* ===== WHY ===== */
.why-section {
  padding: 120px 0;
}

.why-grid {
  max-width: 1300px;
  margin: 0 auto;
  padding: 0 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 20px;
}

.why-card {
  padding: 36px 24px;
  background: rgba(168, 85, 247, 0.06);
  border: 1px solid rgba(255,255,255,0.08);
  border-radius: 20px;
  text-align: center;
  transition: all 0.3s;
}

.why-card:hover {
  border-color: #A855F7;
  transform: translateY(-6px);
  background: rgba(168,85,247,0.1);
}

.why-icon {
  width: 80px;
  height: 80px;
  margin: 0 auto 24px;
  border-radius: 24px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 36px;
}

.why-card h3 { font-size: 1.2rem; font-weight: 700; margin-bottom: 12px; }
.why-card p { font-size: 0.9rem; color: #94a3b8; line-height: 1.7; }

/* ===== 热门教程 ===== */
.popular-section {
  padding: 120px 0;
}

.section-header.row {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  text-align: left;
  max-width: 1300px;
  margin: 0 auto 40px;
  padding: 0 40px;
}

.view-all {
  color: #C084FC !important;
  font-size: 0.95rem !important;
  font-weight: 600 !important;
}

.tutorial-tabs {
  max-width: 1300px;
  margin: 0 auto 40px;
  padding: 0 40px;
  display: flex;
  gap: 10px;
  flex-wrap: wrap;
}

.tab-item {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 10px 20px;
  background: rgba(255,255,255,0.05);
  border: 1px solid rgba(255,255,255,0.08);
  border-radius: 50px;
  cursor: pointer;
  font-size: 0.9rem;
  font-weight: 500;
  color: #94a3b8;
  transition: all 0.3s;
}

.tab-item:hover { border-color: #A855F7; color: #fff; }

.tab-item.active {
  background: linear-gradient(135deg, #A855F7, #EC4899);
  border-color: transparent;
  color: #fff;
  box-shadow: 0 4px 20px rgba(168,85,247,0.3);
}

.tutorial-grid {
  max-width: 1300px;
  margin: 0 auto;
  padding: 0 40px;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
}

.tutorial-card {
  background: rgba(168, 85, 247, 0.06);
  border: 1px solid rgba(255,255,255,0.08);
  border-radius: 20px;
  overflow: hidden;
  cursor: pointer;
  transition: all 0.4s;
}

.tutorial-card:hover {
  transform: translateY(-8px);
  border-color: #A855F7;
  box-shadow: 0 20px 60px rgba(168,85,247,0.2);
}

.tutorial-image {
  height: 180px;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 64px;
}

.tutorial-image::after {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(to bottom, transparent 40%, rgba(7,5,13,1));
}

.difficulty-badge {
  position: absolute;
  top: 12px;
  left: 12px;
  padding: 5px 12px;
  border-radius: 8px;
  font-size: 0.75rem;
  font-weight: 700;
  z-index: 1;
  color: #fff;
}

.level-1, .level-2 { background: #22C55E; }
.level-3 { background: #F59E0B; }
.level-4, .level-5 { background: #EF4444; }

.free-badge {
  position: absolute;
  top: 12px;
  right: 12px;
  padding: 5px 12px;
  background: #22C55E;
  border-radius: 8px;
  font-size: 0.75rem;
  font-weight: 700;
  z-index: 1;
  color: #fff;
}

.tutorial-content { padding: 24px; }

.tutorial-title {
  font-size: 1.15rem;
  font-weight: 700;
  margin-bottom: 10px;
  line-height: 1.4;
}

.tutorial-desc {
  font-size: 0.85rem;
  color: #94a3b8;
  line-height: 1.6;
  margin-bottom: 16px;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.tutorial-meta {
  display: flex;
  gap: 16px;
  font-size: 0.8rem;
  color: #64748b;
  margin-bottom: 16px;
}

.tutorial-author {
  display: flex;
  align-items: center;
  gap: 10px;
  padding-top: 16px;
  border-top: 1px solid rgba(255,255,255,0.06);
}

.author-avatar {
  width: 32px;
  height: 32px;
  border-radius: 50%;
  background: linear-gradient(135deg, #A855F7, #EC4899);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 14px;
  font-weight: 700;
}

.author-name { font-size: 0.85rem; font-weight: 500; }

.author-tag {
  margin-left: auto;
  padding: 4px 10px;
  background: rgba(251,191,36,0.15);
  border-radius: 6px;
  font-size: 0.72rem;
  font-weight: 600;
  color: #FBBF24;
}

/* ===== 学员故事 ===== */
.stories-section {
  padding: 120px 0;
}

.stories-grid {
  max-width: 1300px;
  margin: 0 auto;
  padding: 0 40px;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
}

.story-card {
  padding: 32px;
  background: rgba(168, 85, 247, 0.06);
  border: 1px solid rgba(255,255,255,0.08);
  border-radius: 20px;
  transition: all 0.3s;
}

.story-card:hover {
  border-color: #A855F7;
  transform: translateY(-6px);
}

.story-header {
  display: flex;
  align-items: center;
  gap: 14px;
  margin-bottom: 24px;
}

.story-avatar {
  width: 56px;
  height: 56px;
  border-radius: 16px;
  background: linear-gradient(135deg, #A855F7, #EC4899);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 24px;
}

.story-name { font-weight: 700; font-size: 1.1rem; margin-bottom: 4px; }
.story-role { font-size: 0.8rem; color: #94a3b8; }

.story-text {
  font-size: 0.95rem;
  color: #94a3b8;
  line-height: 1.8;
  margin-bottom: 24px;
  font-style: italic;
}

.story-stats {
  display: flex;
  gap: 24px;
  padding-top: 20px;
  border-top: 1px solid rgba(255,255,255,0.06);
}

.story-stat { text-align: center; flex: 1; }

.stat-value {
  font-size: 1.6rem;
  font-weight: 900;
  background: linear-gradient(135deg, #A855F7, #EC4899);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  margin-bottom: 4px;
}

.stat-label { font-size: 0.8rem; color: #64748b; }

/* ===== CTA ===== */
.cta-section {
  padding: 120px 0;
}

.cta-box {
  max-width: 900px;
  margin: 0 auto;
  padding: 0 40px;
  text-align: center;
}

.cta-box h2 {
  font-size: clamp(2rem, 4vw, 3rem);
  font-weight: 900;
  margin-bottom: 16px;
}

.cta-box p {
  font-size: 1.1rem;
  color: #94a3b8;
  margin-bottom: 40px;
}

.cta-buttons { display: flex; gap: 16px; justify-content: center; flex-wrap: wrap; }

/* ===== 动画 ===== */
.fade-up {
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s cubic-bezier(0.16, 1, 0.3, 1);
}

.fade-up.visible {
  opacity: 1;
  transform: translateY(0);
}

/* ===== 响应式 ===== */
@media (max-width: 1024px) {
  .hero-content { grid-template-columns: 1fr; gap: 60px; }
  .hero-visual { order: -1; }
  .hero-stats { justify-content: center; }
  .track-grid, .tutorial-grid, .stories-grid { grid-template-columns: repeat(2, 1fr); }
  .why-grid { grid-template-columns: repeat(2, 1fr); }
}

@media (max-width: 768px) {
  section { padding: 80px 0; }
  .hero-content { padding: 0 20px; }
  .track-grid, .tutorial-grid, .stories-grid, .why-grid { grid-template-columns: 1fr; }
  .section-header { padding: 0 20px; }
  .section-header.row { flex-direction: column; gap: 20px; text-align: center; align-items: center; }
  .cta-box { padding: 0 20px; }
  .float-card { display: none; }
}
</style>
