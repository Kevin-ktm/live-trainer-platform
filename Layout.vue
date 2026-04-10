<template>
  <div class="layout">
    <!-- 粒子背景 -->
    <div class="bg-particles" id="layoutParticles"></div>
    <div class="bg-orb bg-orb-1"></div>
    <div class="bg-orb bg-orb-2"></div>

    <!-- 顶部导航栏 -->
    <header class="app-header">
      <div class="header-container">
        <!-- Logo -->
        <div class="logo-wrapper">
          <router-link to="/" class="logo-link">
            <div class="logo-container">
              <div class="logo-icon">⭐</div>
              <div class="logo-text">
                <span class="logo-main">星耀学院</span>
                <span class="logo-sub">LIVE ACADEMY</span>
              </div>
            </div>
          </router-link>
        </div>

        <!-- 主导航 -->
        <nav class="main-nav">
          <router-link to="/" class="nav-item" :class="{ active: $route.path === '/' }">
            <span>🏠</span>
            <span>首页</span>
          </router-link>
          <router-link to="/tutorials" class="nav-item" :class="{ active: $route.path.startsWith('/tutorial') }">
            <span>📚</span>
            <span>教程库</span>
          </router-link>
          <router-link to="/categories" class="nav-item" :class="{ active: $route.path === '/categories' }">
            <span>🏷️</span>
            <span>分类</span>
          </router-link>
          <router-link to="/community" class="nav-item" :class="{ active: $route.path === '/community' }">
            <span>💬</span>
            <span>社区</span>
          </router-link>
        </nav>

        <!-- 搜索框 -->
        <div class="search-wrapper">
          <el-input
            v-model="searchKeyword"
            placeholder="搜索教程..."
            clearable
            class="search-input"
            @keyup.enter="handleSearch"
            size="small"
          >
            <template #prefix>
              <span>🔍</span>
            </template>
          </el-input>
        </div>

        <!-- 用户区域 -->
        <div class="user-wrapper">
          <div v-if="!isLoggedIn" class="auth-buttons">
            <el-button type="primary" size="small" @click="router.push('/login')" class="login-btn">
              登录
            </el-button>
            <el-button size="small" @click="router.push('/register')" class="register-btn">
              注册
            </el-button>
          </div>

          <div v-else class="user-info">
            <el-dropdown trigger="click">
              <div class="user-dropdown-trigger">
                <el-avatar
                  :size="32"
                  :src="userStore.profile?.avatar_url || 'https://api.dicebear.com/7.x/avataaars/svg?seed=user'"
                />
                <span class="user-name">{{ userStore.profile?.username || '用户' }}</span>
                <span>▼</span>
              </div>
              <template #dropdown>
                <el-dropdown-menu>
                  <el-dropdown-item @click="router.push('/profile')">个人中心</el-dropdown-item>
                  <el-dropdown-item @click="router.push('/profile?tab=favorites')">我的收藏</el-dropdown-item>
                  <el-dropdown-item @click="router.push('/profile?tab=progress')">学习进度</el-dropdown-item>
                  <el-dropdown-item divided @click="handleLogout">退出登录</el-dropdown-item>
                </el-dropdown-menu>
              </template>
            </el-dropdown>
          </div>
        </div>
      </div>
    </header>

    <!-- 主内容区域 -->
    <main class="app-main">
      <router-view />
    </main>

    <!-- 底部信息 -->
    <footer class="app-footer">
      <div class="footer-container">
        <div class="footer-main">
          <div class="footer-section footer-brand">
            <div class="footer-logo">
              <span class="logo-icon">⭐</span>
              <span class="logo-name">星耀学院</span>
            </div>
            <p class="footer-desc">
              专注娱乐直播培训，涵盖个播、团播、带货全场景。
              助你成为下一颗星。
            </p>
            <div class="footer-socials">
              <a href="#" class="social-btn">𝕏</a>
              <a href="#" class="social-btn">📺</a>
              <a href="#" class="social-btn">📱</a>
            </div>
          </div>

          <div class="footer-section">
            <h4>课程</h4>
            <ul>
              <li><router-link to="/tutorials">全部教程</router-link></li>
              <li><router-link to="/categories">分类浏览</router-link></li>
              <li><router-link to="/search">搜索教程</router-link></li>
              <li><a href="#">热门专题</a></li>
            </ul>
          </div>

          <div class="footer-section">
            <h4>平台</h4>
            <ul>
              <li><a href="#">关于我们</a></li>
              <li><a href="#">导师团队</a></li>
              <li><a href="#">学员故事</a></li>
              <li><a href="#">联系我们</a></li>
            </ul>
          </div>

          <div class="footer-section">
            <h4>支持</h4>
            <ul>
              <li><a href="#">帮助中心</a></li>
              <li><a href="#">用户协议</a></li>
              <li><a href="#">隐私政策</a></li>
              <li><a href="#">商务合作</a></li>
            </ul>
          </div>
        </div>

        <div class="footer-bottom">
          <p>© 2026 星耀学院 · 让每个梦想都被看见</p>
        </div>
      </div>
    </footer>

    <!-- 回到顶部 -->
    <el-backtop :right="40" :bottom="40" target=".app-main" class="back-top">
      <span>↑</span>
    </el-backtop>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'
import { useRouter } from 'vue-router'
import { useUserStore } from '@/stores/user'
import { ElMessage, ElMessageBox } from 'element-plus'

const router = useRouter()
const userStore = useUserStore()
const searchKeyword = ref('')

const isLoggedIn = computed(() => !!userStore.user)

onMounted(() => {
  userStore.initialize()
  initParticles()
})

const initParticles = () => {
  const container = document.getElementById('layoutParticles')
  if (!container) return
  for (let i = 0; i < 20; i++) {
    const p = document.createElement('div')
    p.className = 'particle'
    p.style.left = Math.random() * 100 + '%'
    p.style.animationDelay = Math.random() * 15 + 's'
    p.style.animationDuration = (15 + Math.random() * 10) + 's'
    container.appendChild(p)
  }
}

const handleSearch = () => {
  if (searchKeyword.value.trim()) {
    router.push(`/search?q=${encodeURIComponent(searchKeyword.value)}`)
  }
}

const handleLogout = async () => {
  try {
    await ElMessageBox.confirm('确定要退出登录吗？', '确认退出', { type: 'warning' })
    await userStore.logout()
    ElMessage.success('已退出登录')
    router.push('/')
  } catch {}
}
</script>

<style scoped>
.layout {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  background: #07050D;
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
  opacity: 0.25;
  animation: rise 18s infinite;
}

@keyframes rise {
  0% { transform: translateY(100vh) scale(0); opacity: 0; }
  10% { opacity: 0.25; }
  90% { opacity: 0.25; }
  100% { transform: translateY(-10vh) scale(1); opacity: 0; }
}

.bg-orb {
  position: fixed;
  border-radius: 50%;
  filter: blur(120px);
  opacity: 0.1;
  pointer-events: none;
  z-index: 0;
}

.bg-orb-1 {
  width: 600px;
  height: 600px;
  background: #A855F7;
  top: -200px;
  right: -100px;
}

.bg-orb-2 {
  width: 400px;
  height: 400px;
  background: #EC4899;
  bottom: -100px;
  left: -100px;
}

/* 导航 */
.app-header {
  position: sticky;
  top: 0;
  z-index: 1000;
  background: rgba(7, 5, 13, 0.85);
  backdrop-filter: blur(24px);
  border-bottom: 1px solid rgba(255,255,255,0.06);
}

.header-container {
  max-width: 1300px;
  margin: 0 auto;
  padding: 0 40px;
  height: 70px;
  display: flex;
  align-items: center;
  gap: 40px;
}

.logo-wrapper { flex-shrink: 0; }

.logo-link { text-decoration: none; }

.logo-container {
  display: flex;
  align-items: center;
  gap: 12px;
}

.logo-icon {
  font-size: 28px;
}

.logo-text {
  display: flex;
  flex-direction: column;
}

.logo-main {
  font-size: 1.2rem;
  font-weight: 900;
  background: linear-gradient(135deg, #A855F7, #EC4899);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  line-height: 1.2;
}

.logo-sub {
  font-size: 0.6rem;
  font-weight: 700;
  color: #64748b;
  letter-spacing: 2px;
}

.main-nav {
  display: flex;
  gap: 8px;
  flex: 1;
}

.nav-item {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 10px 20px;
  border-radius: 50px;
  text-decoration: none;
  color: #94a3b8;
  font-size: 0.9rem;
  font-weight: 500;
  transition: all 0.3s;
}

.nav-item:hover {
  color: #fff;
  background: rgba(168, 85, 247, 0.15);
}

.nav-item.active {
  color: #fff;
  background: linear-gradient(135deg, rgba(168,85,247,0.3), rgba(236,72,153,0.3));
}

.search-wrapper { flex: 1; max-width: 260px; }

.search-input :deep(.el-input__wrapper) {
  background: rgba(255,255,255,0.06);
  border: 1px solid rgba(255,255,255,0.08);
  border-radius: 50px;
  box-shadow: none;
  color: #fff;
}

.search-input :deep(.el-input__inner) {
  color: #fff;
}

.auth-buttons { display: flex; gap: 12px; }

.login-btn {
  background: linear-gradient(135deg, #A855F7, #EC4899) !important;
  border: none !important;
  font-weight: 600;
  box-shadow: 0 0 30px rgba(168,85,247,0.3);
}

.register-btn {
  background: rgba(255,255,255,0.06) !important;
  border: 1px solid rgba(255,255,255,0.1) !important;
  color: #fff !important;
}

.user-dropdown-trigger {
  display: flex;
  align-items: center;
  gap: 8px;
  cursor: pointer;
  padding: 6px 12px;
  border-radius: 50px;
  transition: background 0.3s;
  color: #fff;
}

.user-dropdown-trigger:hover {
  background: rgba(168,85,247,0.15);
}

.user-name {
  font-weight: 500;
  max-width: 80px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

/* 主内容 */
.app-main {
  flex: 1;
  position: relative;
  z-index: 1;
}

/* 底部 */
.app-footer {
  background: #0B0A14;
  border-top: 1px solid rgba(255,255,255,0.06);
  padding: 60px 0 30px;
  margin-top: 80px;
  position: relative;
  z-index: 1;
}

.footer-container {
  max-width: 1300px;
  margin: 0 auto;
  padding: 0 40px;
}

.footer-main {
  display: grid;
  grid-template-columns: 2fr 1fr 1fr 1fr;
  gap: 60px;
  margin-bottom: 40px;
}

.footer-logo {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-bottom: 16px;
}

.footer-logo .logo-icon { font-size: 24px; }
.footer-logo .logo-name {
  font-size: 1.2rem;
  font-weight: 800;
  background: linear-gradient(135deg, #A855F7, #EC4899);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.footer-desc {
  color: #64748b;
  font-size: 0.9rem;
  line-height: 1.7;
  margin-bottom: 20px;
}

.footer-socials {
  display: flex;
  gap: 10px;
}

.social-btn {
  width: 38px;
  height: 38px;
  border-radius: 10px;
  background: rgba(255,255,255,0.06);
  border: 1px solid rgba(255,255,255,0.08);
  display: flex;
  align-items: center;
  justify-content: center;
  color: #94a3b8;
  text-decoration: none;
  font-size: 0.9rem;
  transition: all 0.3s;
}

.social-btn:hover {
  background: linear-gradient(135deg, #A855F7, #EC4899);
  border-color: transparent;
  color: #fff;
  transform: translateY(-3px);
}

.footer-section h4 {
  font-size: 0.85rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 1px;
  color: #fff;
  margin-bottom: 20px;
}

.footer-section ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

.footer-section li { margin-bottom: 12px; }

.footer-section a {
  color: #64748b;
  text-decoration: none;
  font-size: 0.9rem;
  transition: color 0.3s;
}

.footer-section a:hover { color: #C084FC; }

.footer-bottom {
  border-top: 1px solid rgba(255,255,255,0.06);
  padding-top: 30px;
  text-align: center;
  color: #475569;
  font-size: 0.85rem;
}

/* 回到顶部 */
.back-top {
  background: linear-gradient(135deg, #A855F7, #EC4899) !important;
  border-radius: 14px !important;
  box-shadow: 0 0 30px rgba(168,85,247,0.4);
  color: #fff;
  font-size: 18px;
  width: 44px !important;
  height: 44px !important;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* 下拉菜单 */
:deep(.el-dropdown-menu) {
  background: #1a1525 !important;
  border: 1px solid rgba(255,255,255,0.1) !important;
  border-radius: 14px !important;
  box-shadow: 0 20px 60px rgba(0,0,0,0.5) !important;
  padding: 8px !important;
}

:deep(.el-dropdown-menu__item) {
  color: #94a3b8 !important;
  border-radius: 8px !important;
  margin: 2px 0 !important;
}

:deep(.el-dropdown-menu__item:hover) {
  background: rgba(168,85,247,0.2) !important;
  color: #fff !important;
}

/* 响应式 */
@media (max-width: 1024px) {
  .header-container { padding: 0 20px; gap: 20px; }
  .main-nav { gap: 4px; }
  .nav-item span:last-child { display: none; }
  .footer-main { grid-template-columns: 1fr 1fr; gap: 40px; }
}

@media (max-width: 768px) {
  .main-nav { display: none; }
  .search-wrapper { display: none; }
  .logo-wrapper { margin-right: auto; }
  .user-name { display: none; }
  .footer-main { grid-template-columns: 1fr; }
}
</style>
