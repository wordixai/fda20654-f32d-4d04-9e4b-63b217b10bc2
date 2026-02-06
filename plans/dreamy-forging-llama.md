# AI 虚拟换衣应用 - 实现计划

## 产品概述

一款时尚感 AI 换衣应用，用户可以上传自己的照片，选择或上传服装图片，AI 生成穿搭效果图。

## 核心用户流程

1. **首页** — 品牌展示 + 核心价值 + 引导用户开始体验
2. **上传人物照片** — 拖拽/点击上传，实时预览
3. **选择服装** — 浏览示例服装库 或 上传自己的服装图片
4. **AI 生成处理** — 动画等待过程，展示处理状态
5. **查看结果** — 生成图展示 + 前后对比滑块 + 下载

## 设计方向

- **风格**: 时尚编辑风，奢华感，深邃优雅
- **色彩**: 深海军蓝(primary) + 香槟金(accent) + 柔玫瑰(点缀) + 奶油白(背景)
- **字体**: Playfair Display(标题/品牌) + Inter(正文/UI)
- **动画**: 渐入上浮、步骤切换、处理中脉冲、结果展示
- **响应式**: 移动端优先，全设备适配

## MVP 功能清单

### 第一步: 设计系统基础
- 更新 `index.css` — CSS 变量(颜色/字体/渐变/动画)
- 更新 `tailwind.config.ts` — 自定义颜色/字体/动画关键帧
- 清理 `App.css` — 移除 #root 的 max-width 约束

**关键文件:**
- `/app/src/index.css`
- `/app/tailwind.config.ts`
- `/app/src/App.css`

### 第二步: 基础类型和数据
- 创建 TypeScript 类型定义 (`src/types/index.ts`)
- 创建示例服装数据 (`src/data/sample-clothing.ts`) — 4个分类(上衣/裙装/外套/裤装)，12-16件样品
- 创建常量和验证 (`src/lib/constants.ts`, `src/lib/validations.ts`)
- 创建图片工具函数 (`src/lib/image-utils.ts`) — 压缩/base64转换

**关键文件:**
- `/app/src/types/index.ts`
- `/app/src/data/sample-clothing.ts`
- `/app/src/lib/constants.ts`
- `/app/src/lib/image-utils.ts`

### 第三步: 共享组件
- `ImageDropzone` — 拖拽上传区域(人物照片/服装均复用)
- `SectionHeading` — 统一的标题+副标题组件
- `Navbar` — 品牌导航栏
- `Footer` — 简约底部

**关键文件:**
- `/app/src/components/shared/ImageDropzone.tsx`
- `/app/src/components/layout/Navbar.tsx`
- `/app/src/components/layout/Footer.tsx`

### 第四步: 着陆页
- `HeroSection` — 全屏 hero，深色渐变背景，大标题 + 金色 CTA
- `HowItWorks` — 三步流程卡片(上传→选择→生成)
- `CTASection` — 底部行动号召
- 更新 `Index.tsx` 组合所有板块

**关键文件:**
- `/app/src/components/landing/HeroSection.tsx`
- `/app/src/components/landing/HowItWorks.tsx`
- `/app/src/components/landing/CTASection.tsx`
- `/app/src/pages/Index.tsx`

### 第五步: 换衣工作流核心
- `useTryOnStore` — Zustand 状态管理(步骤/图片/结果)
- `StepIndicator` — 可视化步骤进度条
- `PersonUpload` — 人物照片上传步骤
- `ClothingCard` — 服装卡片(选中高亮金色边框)
- `ClothingGallery` — 服装库网格+分类筛选
- `ClothingSelector` — 标签页切换(浏览库/自定义上传)
- `TryOn.tsx` — 主工作流页面，AnimatePresence 步骤切换

**关键文件:**
- `/app/src/stores/useTryOnStore.ts`
- `/app/src/components/tryon/StepIndicator.tsx`
- `/app/src/components/tryon/PersonUpload.tsx`
- `/app/src/components/tryon/ClothingSelector.tsx`
- `/app/src/components/tryon/ClothingGallery.tsx`
- `/app/src/pages/TryOn.tsx`

### 第六步: 处理与结果展示
- `ProcessingView` — AI 处理动画(图片汇聚+脉冲环+进度条+状态文字轮播)
- `BeforeAfterSlider` — 前后对比滑块(pointer events 拖拽)
- `ResultView` — 结果展示 + 下载/重试操作按钮
- Mock API — 模拟 AI 返回(延迟后返回占位结果)，便于前端独立开发

**关键文件:**
- `/app/src/components/tryon/ProcessingView.tsx`
- `/app/src/components/tryon/BeforeAfterSlider.tsx`
- `/app/src/components/tryon/ResultView.tsx`
- `/app/src/hooks/useTryOnGeneration.ts`
- `/app/src/lib/api.ts`

### 第七步: 路由和收尾
- 更新 `App.tsx` 添加 `/try-on` 路由 + Toaster
- 添加 Framer Motion 入场动画
- 移动端响应式调优
- SEO meta 标签

**关键文件:**
- `/app/src/App.tsx`

## 设计系统详情

### CSS 变量 (index.css :root)
```
--background: 0 0% 100%
--foreground: 215 50% 10%
--primary: 215 50% 15%          (深海军蓝)
--primary-foreground: 38 60% 95%
--accent: 38 60% 55%            (香槟金)
--accent-foreground: 215 50% 10%
--muted: 220 15% 95%
--muted-foreground: 215 15% 45%
--secondary: 30 20% 96%         (奶油白)
--destructive: 0 84% 60%
--ring: 38 60% 55%
--radius: 0.75rem
```

### 自定义渐变
- `gradient-hero`: 135deg, 深蓝→深蓝偏亮→金色暗调
- `gradient-gold`: 135deg, 金色→浅金色
- `gradient-processing`: 90deg, 深蓝→金→玫瑰(200% background-size 做动画)

### 自定义动画
- `shimmer` — 处理进度条闪烁
- `fade-up` — 板块入场上浮
- `scale-in` — 结果弹入
- `pulse-gold` — 当前步骤脉冲

## AI 后端说明

MVP 阶段使用 **Mock API**:模拟延迟后返回占位图片，前端完整可用。后续可通过 Supabase Edge Function 接入真实 AI API (如 Replicate IDM-VTON 模型)。

## 延后到 V2 的功能

- 用户登录/注册
- 历史记录保存
- 社交分享
- 真实 AI API 接入
- 多语言支持
- 图片裁剪编辑
- 付费/积分系统

## 验证方式

1. `pnpm run build` 确认无编译错误
2. 访问首页查看着陆页所有板块正确渲染
3. 点击 CTA 跳转到 `/try-on`
4. 完整走通上传→选择→生成→查看结果流程
5. 测试拖拽上传和点击上传
6. 测试服装分类筛选
7. 测试前后对比滑块拖拽
8. 测试下载按钮
9. 移动端视口测试响应式布局
