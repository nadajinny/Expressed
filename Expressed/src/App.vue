<template>
  <div :class="['min-h-screen', dark ? 'dark bg-zinc-950 text-white' : 'bg-white text-black']">
    <!-- NAV -->
    <header class="fixed top-0 inset-x-0 z-50 backdrop-blur bg-white/70 dark:bg-black/30 border-b border-black/5 dark:border-white/10">
      <div class="mx-auto max-w-6xl px-4 h-14 flex items-center justify-between">
        <button class="font-semibold tracking-wide" @click="scrollTo('hero')">{{ t.brand }}</button>
        <nav class="hidden md:flex gap-6 text-sm">
          <button v-for="it in navItems" :key="it.id" class="hover:opacity-80" @click="scrollTo(it.id)">{{ it.label }}</button>
        </nav>
        <div class="flex items-center gap-3">
          <button aria-label="Toggle dark mode" @click="dark = !dark" class="p-2 rounded-full border border-black/10 dark:border-white/10">
            <span v-if="dark">☀️</span><span v-else>🌙</span>
          </button>
          <select aria-label="Language" v-model="lang" class="text-sm bg-transparent border border-black/10 dark:border-white/10 rounded px-2 py-1">
            <option value="ko">KO</option>
            <option value="en">EN</option>
          </select>
        </div>
      </div>
    </header>

    <!-- HERO -->
    <section id="hero" class="pt-24 md:pt-28">
      <div class="mx-auto max-w-6xl px-4 grid md:grid-cols-2 gap-8 items-center">
        <div class="animate-fade-in">
          <h1 class="text-3xl md:text-5xl font-bold leading-tight">
            {{ t.title }}
          </h1>
          <p class="mt-4 text-lg md:text-xl opacity-80">{{ t.tagline }}</p>
          <div class="mt-6 flex gap-3">
            <a href="#projects" class="inline-flex items-center gap-2 rounded-xl px-4 py-2 bg-black text-white dark:bg-white dark:text-black">
              ➜ {{ t.ctas.projects }}
            </a>
            <a href="#contact" class="inline-flex items-center gap-2 rounded-xl px-4 py-2 border border-black/10 dark:border-white/20">
              ✉️ {{ t.ctas.contact }}
            </a>
          </div>
          <div class="mt-6 flex gap-4 text-sm opacity-70">
            <span class="inline-flex items-center gap-2">🧠 AI</span>
            <span class="inline-flex items-center gap-2">📱 Mobile</span>
            <span class="inline-flex items-center gap-2">🎮 Game</span>
          </div>
        </div>
        <div class="relative">
          <div class="aspect-[4/3] w-full rounded-3xl bg-gradient-to-br from-indigo-500/20 via-fuchsia-500/20 to-emerald-500/20 dark:from-indigo-400/20 dark:via-fuchsia-400/20 dark:to-emerald-400/20 border border-black/10 dark:border-white/10 overflow-hidden">
            <svg class="absolute inset-0 w-full h-full" viewBox="0 0 600 450" aria-hidden>
              <defs>
                <linearGradient id="g1" x1="0" y1="0" x2="1" y2="1">
                  <stop offset="0%" stop-color="#6366f1" stop-opacity="0.8"/>
                  <stop offset="100%" stop-color="#10b981" stop-opacity="0.8"/>
                </linearGradient>
              </defs>
              <path :d="wavePath" fill="none" stroke="url(#g1)" stroke-width="3">
                <animate attributeName="stroke-dasharray" from="0,1200" to="1200,0" dur="2s" repeatCount="indefinite"/>
              </path>
            </svg>
            <div class="absolute bottom-4 right-4 text-xs md:text-sm opacity-70">Expressed · Code → Beyond</div>
          </div>
        </div>
      </div>
    </section>

    <!-- ABOUT -->
    <section id="about" class="py-16 md:py-20">
      <div class="mx-auto max-w-6xl px-4 grid md:grid-cols-2 gap-8 items-start">
        <div>
          <h2 class="text-2xl md:text-3xl font-semibold mb-6">{{ t.about.h }}</h2>
          <p class="leading-7 opacity-80">{{ t.about.p1 }}</p>
          <p class="leading-7 mt-4 opacity-80">{{ t.about.p2 }}</p>
          <p class="leading-7 mt-4 opacity-80">{{ t.about.p3 }}</p>
        </div>
        <div class="rounded-2xl border border-black/10 dark:border-white/10 p-5">
          <ul class="space-y-3 text-sm">
            <li><strong>Education</strong>: JBNU BS-MS</li>
            <li><strong>Lab</strong>: MacsLab (Medical AI & Computational Science)</li>
            <li><strong>Focus</strong>: Applied AI · Mobile · Games</li>
            <li><strong>Keywords</strong>: Real-time, UX, Systems</li>
          </ul>
          <div class="mt-4 flex gap-3 text-sm">
            <a class="underline" href="https://github.com/nadajinny" target="_blank" rel="noreferrer">GitHub</a>
            <a class="underline" href="https://velog.io/@nadajinny/posts" target="_blank" rel="noreferrer">Velog</a>
            <a class="underline" href="#" target="_blank" rel="noreferrer">LinkedIn</a>
          </div>
        </div>
      </div>
    </section>

    <!-- SKILLS -->
    <section id="skills" class="py-16 md:py-20">
      <div class="mx-auto max-w-6xl px-4">
        <h2 class="text-2xl md:text-3xl font-semibold mb-6">{{ t.skills.h }}</h2>
        <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-6">
          <div class="p-5 rounded-2xl border border-black/10 dark:border-white/10">
            <h3 class="font-semibold mb-4">{{ t.skills.langs }}</h3>
            <div class="space-y-4">
              <SkillBar v-for="s in skillSet.langs" :key="s.name" :name="s.name" :level="s.level" />
            </div>
          </div>
          <div class="p-5 rounded-2xl border border-black/10 dark:border-white/10">
            <h3 class="font-semibold mb-4">{{ t.skills.fw }}</h3>
            <div class="space-y-4">
              <SkillBar v-for="s in skillSet.fw" :key="s.name" :name="s.name" :level="s.level" />
            </div>
          </div>
          <div class="p-5 rounded-2xl border border-black/10 dark:border-white/10">
            <h3 class="font-semibold mb-4">{{ t.skills.db }}</h3>
            <div class="space-y-4">
              <SkillBar v-for="s in skillSet.db" :key="s.name" :name="s.name" :level="s.level" />
            </div>
          </div>
          <div class="p-5 rounded-2xl border border-black/10 dark:border-white/10">
            <h3 class="font-semibold mb-4">{{ t.skills.tools }}</h3>
            <div class="space-y-4">
              <SkillBar v-for="s in skillSet.tools" :key="s.name" :name="s.name" :level="s.level" />
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- PROJECTS -->
    <section id="projects" class="py-16 md:py-20">
      <div class="mx-auto max-w-6xl px-4">
        <h2 class="text-2xl md:text-3xl font-semibold mb-6">{{ t.projects.h }}</h2>
        <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
          <article v-for="p in projectList" :key="p.id" class="group rounded-2xl overflow-hidden border border-black/10 dark:border-white/10 bg-white/60 dark:bg-white/5">
            <div class="aspect-video overflow-hidden">
              <img :src="p.img" :alt="p.title" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-500" />
            </div>
            <div class="p-4">
              <h3 class="font-semibold text-lg">{{ p.title }}</h3>
              <p class="mt-1 text-sm opacity-80">{{ lang === 'ko' ? p.desc_ko : p.desc_en }}</p>
              <div class="mt-3 flex flex-wrap gap-2">
                <span v-for="s in p.stack" :key="s" class="text-xs px-2 py-1 rounded-full border border-black/10 dark:border-white/15">{{ s }}</span>
              </div>
              <div class="mt-4 flex gap-3 text-sm">
                <a v-if="p.links.demo" :href="p.links.demo" target="_blank" class="underline">Demo ↗</a>
                <a v-if="p.links.repo" :href="p.links.repo" target="_blank" class="underline">Repo ↗</a>
              </div>
            </div>
          </article>
        </div>
      </div>
    </section>

    <!-- TIMELINE -->
    <section id="timeline" class="py-16 md:py-20">
      <div class="mx-auto max-w-6xl px-4">
        <h2 class="text-2xl md:text-3xl font-semibold mb-6">{{ t.timeline.h }}</h2>
        <ol class="relative border-s border-black/10 dark:border-white/10 ml-3">
          <li v-for="(item,i) in timelineList" :key="i" class="mb-10 ms-6">
            <span class="absolute -start-3 mt-1.5 flex h-6 w-6 items-center justify-center rounded-full bg-black text-white dark:bg-white dark:text-black text-xs">{{ i+1 }}</span>
            <div class="p-4 rounded-xl border border-black/10 dark:border-white/10">
              <div class="text-xs opacity-70">{{ item.date }}</div>
              <div class="font-semibold mt-1">{{ lang==='ko' ? item.title_ko : item.title_en }}</div>
              <div class="text-sm opacity-80 mt-1">{{ lang==='ko' ? item.detail_ko : item.detail_en }}</div>
            </div>
          </li>
        </ol>
      </div>
    </section>

    <!-- BLOG -->
    <section id="blog" class="py-16 md:py-20">
      <div class="mx-auto max-w-6xl px-4">
        <h2 class="text-2xl md:text-3xl font-semibold mb-6">{{ t.blog.h }}</h2>
        <div class="grid md:grid-cols-3 gap-6">
          <a v-for="p in postList" :key="p.id" :href="p.url" target="_blank" class="p-4 rounded-2xl border border-black/10 dark:border-white/10 hover:bg-black/5 dark:hover:bg-white/5 transition">
            <div class="font-medium">{{ p.title }}</div>
            <div class="mt-2 inline-flex items-center gap-1 text-sm underline opacity-80">{{ t.blog.more }} ↗</div>
          </a>
        </div>
      </div>
    </section>

    <!-- CONTACT -->
    <section id="contact" class="py-16 md:py-20">
      <div class="mx-auto max-w-6xl px-4 grid md:grid-cols-2 gap-8 items-start">
        <div>
          <h2 class="text-2xl md:text-3xl font-semibold mb-6">{{ t.contact.h }}</h2>
          <form @submit.prevent="onSubmit" class="space-y-4">
            <div>
              <label class="text-sm opacity-80">{{ t.contact.form.name }}</label>
              <input required class="mt-1 w-full rounded-xl border border-black/10 dark:border-white/10 bg-transparent px-3 py-2" />
            </div>
            <div>
              <label class="text-sm opacity-80">{{ t.contact.form.email }}</label>
              <input type="email" required class="mt-1 w-full rounded-xl border border-black/10 dark:border-white/10 bg-transparent px-3 py-2" />
            </div>
            <div>
              <label class="text-sm opacity-80">{{ t.contact.form.msg }}</label>
              <textarea required rows="5" class="mt-1 w-full rounded-xl border border-black/10 dark:border-white/10 bg-transparent px-3 py-2" />
            </div>
            <button class="inline-flex items-center gap-2 rounded-xl px-4 py-2 bg-black text-white dark:bg-white dark:text-black">
              ✉️ {{ t.contact.form.send }}
            </button>
            <div v-if="sent" class="text-sm opacity-80">Thank you! I will get back to you soon.</div>
          </form>
        </div>
        <div class="rounded-2xl border border-black/10 dark:border-white/10 p-5">
          <h3 class="font-semibold mb-3">{{ t.contact.links }}</h3>
          <ul class="space-y-2 text-sm">
            <li class="inline-flex items-center gap-2">✉️ <a href="mailto:jinsun23007@gmail.com" class="underline">jinsun23007@gmail.com</a></li>
            <li class="inline-flex items-center gap-2">💻 <a class="underline" href="https://github.com/nadajinny" target="_blank">github.com/nadajinny</a></li>
            <li class="inline-flex items-center gap-2">🌐 <a class="underline" href="https://velog.io/@nadajinny/posts" target="_blank">velog.io/@nadajinny</a></li>
          </ul>
        </div>
      </div>
    </section>

    <footer class="py-10 text-center text-sm opacity-70 border-t border-black/5 dark:border-white/10 mt-10">
      {{ t.footer }}
    </footer>
  </div>
</template>

<script setup lang="ts">
import { computed, onMounted, ref } from 'vue'

// i18n-like copy
const strings = {
  ko: {
    brand: 'Expressed',
    nav: { hero: '홈', about: '소개', skills: '기술 스택', projects: '프로젝트', timeline: '이력/연혁', blog: '블로그/아카이브', contact: '연락처' },
    title: '나다 이 | AI·모바일·게임 개발자',
    tagline: '코드를 통해 세상을 표현하는 개발자',
    ctas: { projects: '프로젝트 보기', contact: '연락하기' },
    about: {
      h: 'About Me',
      p1: '전북대학교 컴퓨터공학·인공지능공학 전공, MacsLab 학부 연구생으로 활동 중입니다. AI × 모바일 × 게임의 교차점에서 사용자 경험을 만드는 데 관심이 많습니다.',
      p2: '가치관은 “문제를 맥락 속에서 바라보고, 작은 반복으로 큰 변화를 만든다”. 실시간 데이터와 사용자 상호작용을 결합하는 제품을 즐겨 만듭니다.',
      p3: '취미는 러닝과 게임 메카닉 분석, 그리고 개발 블로그 쓰기입니다.'
    },
    skills: { h: 'Skill Stack', langs: '언어', fw: '프레임워크/라이브러리', db: '데이터베이스/백엔드', tools: '툴/플랫폼' },
    projects: { h: '대표 프로젝트', more: '자세히 보기' },
    timeline: { h: '이력/연혁' },
    blog: { h: '블로그/연구 아카이브', more: '글 보기' },
    contact: { h: 'Contact', form: { name: '이름', email: '이메일', msg: '메시지', send: '보내기' }, links: '바로가기' },
    footer: '© 2025 nadajinny — Expressed'
  },
  en: {
    brand: 'Expressed',
    nav: { hero: 'Home', about: 'About', skills: 'Skills', projects: 'Projects', timeline: 'Timeline', blog: 'Blog/Archive', contact: 'Contact' },
    title: 'Nada Lee | AI · Mobile · Game Developer',
    tagline: 'A developer expressing the world through code',
    ctas: { projects: 'View Projects', contact: 'Contact' },
    about: {
      h: 'About Me',
      p1: 'BS-MS student at JBNU and undergraduate RA at MacsLab. I love building at the intersection of AI × mobile × games.',
      p2: 'Values: “See problems in context and create change with small iterations.” I enjoy combining real-time data with user interaction.',
      p3: 'Hobbies: running, dissecting game mechanics, and writing dev blogs.'
    },
    skills: { h: 'Skill Stack', langs: 'Languages', fw: 'Frameworks/Libraries', db: 'Databases/Backend', tools: 'Tools/Platforms' },
    projects: { h: 'Featured Projects', more: 'Details' },
    timeline: { h: 'Timeline' },
    blog: { h: 'Blog/Research Archive', more: 'Read' },
    contact: { h: 'Contact', form: { name: 'Name', email: 'Email', msg: 'Message', send: 'Send' }, links: 'Quick Links' },
    footer: '© 2025 nadajinny — Expressed'
  }
} as const

// data
const projectList = [
  {
    id: 'justrip',
    title: 'JusTrip',
    desc_ko: '실시간 날씨 기반 AI 여행 추천 웹앱 (UNLV × JNU 해커톤)',
    desc_en: 'AI travel recommendations powered by real-time weather (UNLV × JNU Hackathon)',
    stack: ['Vue 3', 'OpenWeather', 'Vertex AI'],
    img: 'https://images.unsplash.com/photo-1500530855697-b586d89ba3ee?q=80&w=1200&auto=format&fit=crop',
    links: { demo: '#', repo: 'https://github.com/nadajinny/JusTrip' }
  },
  {
    id: 'medi-mate',
    title: 'Medi-Mate',
    desc_ko: '실시간 음성 요약 기반 진료 기록 앱 (RN + FastAPI)',
    desc_en: 'Real-time voice summarization for clinical notes (RN + FastAPI)',
    stack: ['React Native', 'WebSocket', 'VITO STT', 'FastAPI'],
    img: 'https://images.unsplash.com/photo-1586773860418-d37222d8fce3?q=80&w=1200&auto=format&fit=crop',
    links: { demo: '#', repo: 'https://github.com/nadajinny' }
  },
  {
    id: 'omok-ai',
    title: 'Omok AI',
    desc_ko: '알파-베타 + 패턴 평가로 오목 AI 구현',
    desc_en: 'Gomoku AI with alpha-beta pruning and pattern evaluation',
    stack: ['Python', 'Search', 'Heuristics'],
    img: 'https://images.unsplash.com/photo-1607706189992-eae578626c86?q=80&w=1200&auto=format&fit=crop',
    links: { demo: '#', repo: 'https://github.com/nadajinny' }
  }
]

const postList = [
  { id: 'velog-1', title: 'React Native 음성 인식 실시간 스트림 삽질기', url: 'https://velog.io/@nadajinny/posts' },
  { id: 'ai-1', title: '베이지안 네트워크 추론: Enumeration vs Variable Elimination', url: 'https://velog.io/@nadajinny/posts' },
  { id: 'cn-1', title: '컴퓨터네트워크: Top-Down Approach 정리', url: 'https://velog.io/@nadajinny/posts' }
]

const skillSet = {
  langs: [
    { name: 'Python', level: 85 },
    { name: 'JavaScript/TypeScript', level: 80 },
    { name: 'GDScript', level: 70 }
  ],
  fw: [
    { name: 'Vue / React / Next', level: 85 },
    { name: 'React Native', level: 80 },
    { name: 'Flutter', level: 70 }
  ],
  db: [
    { name: 'Firebase', level: 75 },
    { name: 'Supabase', level: 65 }
  ],
  tools: [
    { name: 'Git/GitHub', level: 85 },
    { name: 'FastAPI', level: 70 }
  ]
}

const timelineList = [
  { date: '2025.01 – 현재', title_ko: 'MacsLab 학부 연구생', title_en: 'Undergraduate RA @ MacsLab', detail_ko: '실시간 AI 모바일 앱 개발 및 데이터 연동', detail_en: 'Built real-time AI mobile app and integrations' },
  { date: '2025.06', title_ko: 'JusTrip 프로젝트', title_en: 'JusTrip Project', detail_ko: '실시간 날씨 × AI 추천 웹앱', detail_en: 'Real-time weather × AI recommendations' },
  { date: '2023.03 – 2026.08(예정)', title_ko: '전북대 컴퓨터공학·인공지능공학', title_en: 'JBNU CS & AI Eng.', detail_ko: 'BS-MS 통합과정', detail_en: 'BS-MS integrated program' }
]

// state
const lang = ref<'ko' | 'en'>('ko')
const dark = ref(true)
const sent = ref(false)

// computed / helpers
const t = computed(() => strings[lang.value])
const navItems = computed(() => [
  { id: 'hero', label: t.value.nav.hero },
  { id: 'about', label: t.value.nav.about },
  { id: 'skills', label: t.value.nav.skills },
  { id: 'projects', label: t.value.nav.projects },
  { id: 'timeline', label: t.value.nav.timeline },
  { id: 'blog', label: t.value.nav.blog },
  { id: 'contact', label: t.value.nav.contact }
])

const wavePath = 'M0 300 Q 150 200 300 300 T 600 300'

function scrollTo(id: string) {
  document.getElementById(id)?.scrollIntoView({ behavior: 'smooth', block: 'start' })
}

function onSubmit() {
  // TODO: EmailJS 또는 API 연동
  sent.value = true
}

onMounted(() => {
  document.documentElement.style.scrollBehavior = 'smooth'
})
</script>

<script lang="ts">
export default { name: 'App' }
</script>

<style scoped>
/* simple fade-in animation */
@keyframes fade-in { from { opacity: 0; transform: translateY(8px);} to { opacity: 1; transform: translateY(0);} }
.animate-fade-in { animation: fade-in .7s ease-out both; }

/* utility fallbacks when Tailwind 미사용 시 */
.bg-white{ background:#fff; }
.text-black{ color:#111; }
.bg-zinc-950{ background:#0a0a0a; }
.text-white{ color:#fff; }
.border{ border-width:1px; }
.rounded-3xl{ border-radius:1.5rem; }
.rounded-2xl{ border-radius:1rem; }
.rounded-xl{ border-radius:.75rem; }
.aspect-[4\/3]{ position:relative; padding-bottom:75%; }
.aspect-[4\/3]>*{ position:absolute; inset:0; }
/* (실제 프로젝트에서는 Tailwind 추천) */
</style>

<!--
설치/사용 가이드(요약)
1) Vite Vue + TS 템플릿 생성:  npm create vite@latest expressed -- --template vue-ts
2) 위 파일 구조로 저장
   - src/main.ts  (상단 main.ts 부분 복사)
   - src/App.vue  (본 파일 저장)
3) 실행: npm i && npm run dev
4) Tailwind 사용할 경우: 
   npm i -D tailwindcss postcss autoprefixer && npx tailwindcss init -p
   tailwind.config.cjs 의 content 에 "./index.html","./src/**/*.{vue,ts}" 추가
   src/assets/main.css에 @tailwind base; @tailwind components; @tailwind utilities; 입력 후 main.ts에서 import
-->
