<template>
  <div class="home-container">
    <div class="planner-page">
      <div class="top-banner">
        <div class="top-banner-content">
          <div class="banner-kicker"><span></span> YOUR NEXT CHAPTER</div>
          <h1>把向往的远方，<br />变成<span>下一站。</span></h1>
          <p>从一座心动的城市开始。让 AI 为你安排风景、美食与休憩，<br class="desktop-break" />把时间留给旅途中的美好。</p>
          <div class="hero-features"><span><CompassOutlined /> 专属行程</span><span><WalletOutlined /> 预算规划</span><span><EnvironmentOutlined /> 地图路线</span></div>
        </div>
        <div class="travel-illustration" aria-hidden="true">
          <div class="journey-stamp">LET’S GO<br /><span>探索 · 发现 · 出发</span></div>
          <div class="landscape-card">
            <svg viewBox="0 0 460 260" fill="none"><rect width="460" height="260" fill="#e5eddf"/><circle cx="335" cy="66" r="31" fill="#eab778"/><path d="M0 204L111 65L218 202L308 117L460 230V260H0Z" fill="#a7bea0"/><path d="M0 228L154 138L279 227L369 166L460 218V260H0Z" fill="#5e8d77"/><path d="M0 250C90 185 127 239 210 210C305 178 336 215 460 195V260H0Z" fill="#2e6955"/><path d="M257 260C340 229 195 221 251 203" stroke="#e5eacb" stroke-width="10"/><path d="M62 78Q103 51 143 61M181 44Q215 24 244 40" stroke="#fffef4" stroke-width="4" stroke-linecap="round"/></svg>
            <div class="landscape-caption"><span>去山野，也去人间烟火</span><span>EXPLORE MORE ↗</span></div>
          </div>
          <div class="journey-note"><span class="note-icon"><EnvironmentOutlined /></span><div>下一站，随心出发<small>你的旅程，由你定义</small></div><span class="note-spark">✦</span></div>
        </div>
      </div>

      <div class="planning-steps" aria-label="规划步骤"><span class="step-current"><b>01</b> 告诉我们你的想法</span><span class="step-line"></span><span><b>02</b> AI 定制专属行程</span><span class="step-line"></span><span><b>03</b> 带上期待出发</span></div>
      <a-card class="form-card" :bordered="false">
        <div class="form-card-header">
          <div>
            <div class="form-eyebrow">LET’S PLAN YOUR TRIP</div>
            <h2>你的旅行，你来定义<span>填写偏好，剩下的交给我们</span></h2>
          </div>
          <div class="header-status">
            <span>{{ formData.city || '未选择城市' }}</span>
            <span>{{ formData.travel_days }} 天</span>
            <span>{{ formData.party.total }} 人</span>
          </div>
        </div>

        <a-form
          :model="formData"
          layout="vertical"
          @finish="handleSubmit"
        >
          <div class="form-section">
            <div class="section-header"><span class="section-number">01</span>
              <EnvironmentOutlined />
              <span class="section-title">目的地与日期</span>
            </div>

            <a-row :gutter="[20, 16]">
              <a-col :xs="{ span: 24 }" :lg="{ span: 10 }">
                <a-form-item name="city" :rules="[{ required: true, message: '请输入目的地城市' }]">
                  <template #label>
                    <span class="form-label">目的地城市</span>
                  </template>
                  <a-input
                    v-model:value="formData.city"
                    placeholder="想去哪里？例如：杭州"
                    size="large"
                    class="custom-input"
                  />
                  <div class="city-suggestions"><span>灵感目的地</span><button v-for="city in ['北京', '杭州', '成都', '大理']" :key="city" type="button" :aria-pressed="formData.city === city" @click="formData.city = city">{{ city }}</button></div>
                </a-form-item>
              </a-col>
              <a-col :xs="{ span: 24 }" :sm="{ span: 12 }" :lg="{ span: 7 }">
                <a-form-item name="start_date" :rules="[{ required: true, message: '请选择开始日期' }]">
                  <template #label>
                    <span class="form-label">开始日期</span>
                  </template>
                  <a-date-picker
                    v-model:value="formData.start_date"
                    style="width: 100%"
                    size="large"
                    class="custom-input"
                    placeholder="选择日期"
                  />
                </a-form-item>
              </a-col>
              <a-col :xs="{ span: 24 }" :sm="{ span: 12 }" :lg="{ span: 7 }">
                <a-form-item name="end_date" :rules="[{ required: true, message: '请选择结束日期' }]">
                  <template #label>
                    <span class="form-label">结束日期</span>
                  </template>
                  <a-date-picker
                    v-model:value="formData.end_date"
                    style="width: 100%"
                    size="large"
                    class="custom-input"
                    placeholder="选择日期"
                  />
                </a-form-item>
              </a-col>
            </a-row>
          </div>

          <div class="form-section">
            <div class="section-header"><span class="section-number">02</span>
              <TeamOutlined />
              <span class="section-title">同行与预算</span>
            </div>

            <a-row :gutter="[20, 16]">
              <a-col :xs="{ span: 8 }" :md="{ span: 4 }">
                <a-form-item name="adults">
                  <template #label>
                    <span class="form-label">成人</span>
                  </template>
                  <a-input-number v-model:value="formData.party.adults" :min="0" :max="20" size="large" class="custom-input" style="width: 100%" />
                </a-form-item>
              </a-col>
              <a-col :xs="{ span: 8 }" :md="{ span: 4 }">
                <a-form-item name="children">
                  <template #label>
                    <span class="form-label">儿童</span>
                  </template>
                  <a-input-number v-model:value="formData.party.children" :min="0" :max="20" size="large" class="custom-input" style="width: 100%" />
                </a-form-item>
              </a-col>
              <a-col :xs="{ span: 8 }" :md="{ span: 4 }">
                <a-form-item name="elders">
                  <template #label>
                    <span class="form-label">老人</span>
                  </template>
                  <a-input-number v-model:value="formData.party.elders" :min="0" :max="20" size="large" class="custom-input" style="width: 100%" />
                </a-form-item>
              </a-col>
              <a-col :xs="{ span: 24 }" :md="{ span: 4 }">
                <a-form-item name="companion_type">
                  <template #label>
                  <span class="form-label">同行类型</span>
                </template>
                <a-select v-model:value="formData.party.companion_type" size="large" class="custom-select">
                    <a-select-option
                      v-for="option in companionTypeOptions"
                      :key="option.value"
                      :value="option.value"
                    >
                      {{ option.label }}
                    </a-select-option>
                  </a-select>
                </a-form-item>
              </a-col>
              <a-col :xs="{ span: 24 }" :md="{ span: 4 }">
                <a-form-item name="budget_amount">
                  <template #label>
                    <span class="form-label">总预算 / 元</span>
                  </template>
                  <a-input-number
                    v-model:value="formData.budget_constraint.amount"
                    :min="0"
                    :step="100"
                    size="large"
                    class="custom-input"
                    style="width: 100%"
                    placeholder="可不填"
                  />
                </a-form-item>
              </a-col>
              <a-col :xs="{ span: 24 }" :md="{ span: 4 }">
                <a-form-item name="budget_level">
                  <template #label>
                  <span class="form-label">预算档位</span>
                </template>
                <a-select v-model:value="formData.budget_constraint.budget_level" size="large" class="custom-select">
                    <a-select-option
                      v-for="option in budgetLevelOptions"
                      :key="option.value"
                      :value="option.value"
                    >
                      {{ option.label }}
                    </a-select-option>
                  </a-select>
                </a-form-item>
              </a-col>
            </a-row>
          </div>

          <div class="form-section">
            <div class="section-header"><span class="section-number">03</span>
              <CarOutlined />
              <span class="section-title">偏好设置</span>
            </div>

            <a-row :gutter="[20, 16]">
              <a-col :xs="{ span: 24 }" :lg="{ span: 12 }">
                <a-form-item name="transportation">
                  <template #label>
                  <span class="form-label">交通方式</span>
                </template>
                <a-select v-model:value="formData.transportation" size="large" class="custom-select">
                    <a-select-option
                      v-for="option in transportationOptions"
                      :key="option.value"
                      :value="option.value"
                    >
                      {{ option.label }}
                    </a-select-option>
                  </a-select>
                </a-form-item>
              </a-col>
              <a-col :xs="{ span: 24 }" :lg="{ span: 12 }">
                <a-form-item name="accommodation">
                  <template #label>
                  <span class="form-label">住宿偏好</span>
                </template>
                <a-select v-model:value="formData.accommodation" size="large" class="custom-select">
                    <a-select-option
                      v-for="option in accommodationOptions"
                      :key="option.value"
                      :value="option.value"
                    >
                      {{ option.label }}
                    </a-select-option>
                  </a-select>
                </a-form-item>
              </a-col>
              <a-col :span="24">
                <a-form-item name="preferences">
                  <template #label>
                    <span class="form-label">旅途中，你更期待什么？ <span class="optional-label">可多选</span></span>
                  </template>
                  <div class="preference-tags">
                    <a-checkbox-group v-model:value="formData.preferences" class="custom-checkbox-group">
                      <a-checkbox
                        v-for="option in preferenceOptions"
                        :key="option.value"
                        :value="option.value"
                        class="preference-tag"
                      >
                        <span class="preference-icon">{{ option.icon }}</span>
                        <span>{{ option.label }}</span>
                      </a-checkbox>
                    </a-checkbox-group>
                  </div>
                </a-form-item>
              </a-col>
            </a-row>
          </div>

          <div class="form-section">
            <div class="section-header"><span class="section-number">04</span>
              <EditOutlined />
              <span class="section-title">额外要求</span>
            </div>

            <a-form-item name="free_text_input">
              <a-textarea
                v-model:value="formData.free_text_input"
                placeholder="还有什么小心愿？比如想看一场日出、带长辈慢慢逛，或需要避开某些食材……"
                :rows="3"
                size="large"
                class="custom-textarea"
              />
            </a-form-item>
          </div>

          <div class="submit-summary"><span><EnvironmentOutlined /> {{ formData.city || '目的地待定' }} <i>·</i> {{ formData.travel_days }} 天 <i>·</i> {{ formData.party.total }} 人同行</span><span>一份专属于你的旅行提案</span></div>
          <a-form-item>
            <a-button
              type="primary"
              html-type="submit"
              :loading="loading"
              size="large"
              block
              class="submit-button"
            >
              <template v-if="!loading">
                <RocketOutlined />
                <span>生成我的专属行程</span><span class="submit-arrow">↗</span>
              </template>
              <template v-else>
                <span>正在生成中...</span>
              </template>
            </a-button>
          </a-form-item>

          <a-form-item v-if="loading">
            <div class="loading-container" role="status" aria-live="polite">
              <a-progress
                :percent="loadingProgress"
                status="active"
                :stroke-color="{
                  '0%': '#0f766e',
                  '100%': '#a4b984',
                }"
                :stroke-width="8"
              />
              <p class="loading-status">
                {{ loadingStatus }}
              </p>
            </div>
          </a-form-item>
        </a-form>
      </a-card>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, reactive, watch } from 'vue'
import { useRouter } from 'vue-router'
import { message } from 'ant-design-vue'
import {
  CarOutlined,
  CompassOutlined,
  EditOutlined,
  EnvironmentOutlined,
  RocketOutlined,
  TeamOutlined,
  WalletOutlined
} from '@ant-design/icons-vue'
import { generateTripPlan } from '@/services/api'
import type { TripFormData } from '@/types'
import type { Dayjs } from 'dayjs'

const router = useRouter()
const loading = ref(false)
const loadingProgress = ref(0)
const loadingStatus = ref('')

const companionTypeOptions = [
  { label: '独行', value: 'solo' },
  { label: '情侣', value: 'couple' },
  { label: '朋友', value: 'friends' },
  { label: '亲子', value: 'family_with_children' },
  { label: '带长辈', value: 'family_with_elders' },
  { label: '商务', value: 'business' },
  { label: '其他', value: 'other' }
]

const budgetLevelOptions = [
  { label: '节省', value: 'limited' },
  { label: '标准', value: 'standard' },
  { label: '舒适', value: 'comfortable' },
  { label: '高端', value: 'premium' },
  { label: '奢华', value: 'luxury' }
]

const transportationOptions = [
  { label: '公共交通', value: '公共交通' },
  { label: '地铁公交', value: '地铁公交' },
  { label: '打车/网约车', value: '打车/网约车' },
  { label: '自驾', value: '自驾' },
  { label: '租车自驾', value: '租车自驾' },
  { label: '包车/私人司机', value: '包车/私人司机' },
  { label: '高铁+市内交通', value: '高铁+市内交通' },
  { label: '飞机+市内交通', value: '飞机+市内交通' },
  { label: '骑行/步行', value: '骑行/步行' },
  { label: '混合交通', value: '混合交通' },
  { label: '无障碍交通优先', value: '无障碍交通优先' }
]

const accommodationOptions = [
  { label: '经济型酒店', value: '经济型酒店' },
  { label: '舒适型酒店', value: '舒适型酒店' },
  { label: '高端酒店', value: '高端酒店' },
  { label: '豪华酒店', value: '豪华酒店' },
  { label: '亲子酒店', value: '亲子酒店' },
  { label: '民宿', value: '民宿' }
]

const preferenceOptions = [
  { label: '历史文化', value: '历史文化', icon: '🏛️' },
  { label: '自然风光', value: '自然风光', icon: '🏞️' },
  { label: '美食探店', value: '美食', icon: '🍜' },
  { label: '购物商圈', value: '购物', icon: '🛍️' },
  { label: '艺术展览', value: '艺术', icon: '🎨' },
  { label: '休闲放松', value: '休闲', icon: '☕' },
  { label: '亲子友好', value: '亲子友好', icon: '🧸' },
  { label: '老人友好', value: '老人友好', icon: '🧓' },
  { label: '小众路线', value: '小众路线', icon: '🧭' },
  { label: '夜游体验', value: '夜游', icon: '🌃' },
  { label: '摄影打卡', value: '摄影打卡', icon: '📷' },
  { label: '博物馆', value: '博物馆', icon: '🏺' },
  { label: '城市漫步', value: '城市漫步', icon: '🚶' },
  { label: '户外徒步', value: '户外徒步', icon: '🥾' },
  { label: '主题乐园', value: '主题乐园', icon: '🎢' },
  { label: '避开人群', value: '避开人群', icon: '🌿' }
]

type TripFormState = Omit<TripFormData, 'start_date' | 'end_date'> & {
  start_date: Dayjs | null
  end_date: Dayjs | null
}

const formData = reactive<TripFormState>({
  city: '',
  start_date: null,
  end_date: null,
  travel_days: 1,
  transportation: '公共交通',
  accommodation: '经济型酒店',
  preferences: [],
  free_text_input: '',
  party: {
    adults: 1,
    children: 0,
    elders: 0,
    total: 1,
    companion_type: 'solo'
  },
  budget_constraint: {
    amount: null,
    scope: 'total',
    currency: 'CNY',
    budget_level: 'standard',
    strictness: 'none'
  }
})

// 监听日期变化,自动计算旅行天数
watch([() => formData.start_date, () => formData.end_date], ([start, end]) => {
  if (start && end) {
    const days = end.diff(start, 'day') + 1
    if (days > 0 && days <= 30) {
      formData.travel_days = days
    } else if (days > 30) {
      message.warning('旅行天数不能超过30天')
      formData.end_date = null
    } else {
      message.warning('结束日期不能早于开始日期')
      formData.end_date = null
    }
  }
})

// planner协议要求party.total显式等于成人、儿童、老人之和
watch([() => formData.party.adults, () => formData.party.children, () => formData.party.elders], ([adults, children, elders]) => {
  const adultCount = Number(adults || 0)
  const childCount = Number(children || 0)
  const elderCount = Number(elders || 0)
  formData.party.total = adultCount + childCount + elderCount
  if (childCount > 0) {
    formData.party.companion_type = 'family_with_children'
  } else if (elderCount > 0) {
    formData.party.companion_type = 'family_with_elders'
  } else if (adultCount === 1) {
    formData.party.companion_type = 'solo'
  } else if (adultCount === 2) {
    formData.party.companion_type = 'couple'
  } else if (adultCount > 2) {
    formData.party.companion_type = 'friends'
  }
})

const handleSubmit = async () => {
  if (!formData.start_date || !formData.end_date) {
    message.error('请选择日期')
    return
  }

  if (formData.party.total <= 0) {
    message.error('同行人数至少为1人')
    return
  }

  loading.value = true
  loadingProgress.value = 0
  loadingStatus.value = '正在初始化...'

  // 模拟进度更新
  const progressInterval = setInterval(() => {
    if (loadingProgress.value < 90) {
      loadingProgress.value += 10

      // 更新状态文本
      if (loadingProgress.value <= 30) {
        loadingStatus.value = '🔍 正在搜索景点...'
      } else if (loadingProgress.value <= 50) {
        loadingStatus.value = '🌤️ 正在查询天气...'
      } else if (loadingProgress.value <= 70) {
        loadingStatus.value = '🏨 正在推荐酒店...'
      } else {
        loadingStatus.value = '📋 正在生成行程计划...'
      }
    }
  }, 500)

  try {
    const budgetAmount = formData.budget_constraint.amount
    const budgetStrictness = budgetAmount === null || budgetAmount === undefined ? 'none' : 'soft'
    const requestData: TripFormData = {
      city: formData.city,
      start_date: formData.start_date.format('YYYY-MM-DD'),
      end_date: formData.end_date.format('YYYY-MM-DD'),
      travel_days: formData.travel_days,
      transportation: formData.transportation,
      accommodation: formData.accommodation,
      preferences: formData.preferences,
      free_text_input: formData.free_text_input,
      party: {
        adults: formData.party.adults,
        children: formData.party.children,
        elders: formData.party.elders,
        total: formData.party.total,
        companion_type: formData.party.companion_type
      },
      budget_constraint: {
        amount: budgetAmount ?? null,
        scope: 'total',
        currency: 'CNY',
        budget_level: formData.budget_constraint.budget_level,
        strictness: budgetStrictness
      }
    }

    const response = await generateTripPlan(requestData)

    clearInterval(progressInterval)
    loadingProgress.value = 100
    loadingStatus.value = '✅ 完成!'

    if (response.success && response.data) {
      // 保存到sessionStorage
      sessionStorage.setItem('tripPlan', JSON.stringify(response.data))

      message.success('旅行计划生成成功!')

      // 短暂延迟后跳转
      setTimeout(() => {
        router.push('/result')
      }, 500)
    } else {
      message.error(response.message || '生成失败')
    }
  } catch (error: any) {
    clearInterval(progressInterval)
    message.error(error.message || '生成旅行计划失败,请稍后重试')
  } finally {
    setTimeout(() => {
      loading.value = false
      loadingProgress.value = 0
      loadingStatus.value = ''
    }, 1000)
  }
}
</script>

<style scoped>
.home-container { padding: 42px 40px 64px; }
.planner-page { max-width: 1160px; margin: auto; }
.top-banner { display: grid; grid-template-columns: 1.15fr 1fr; align-items: center; gap: 60px; min-height: 340px; margin-bottom: 38px; }
.banner-kicker { display: flex; align-items: center; gap: 9px; color: var(--forest); font-size: 11px; font-weight: 700; letter-spacing: 2.3px; }
.banner-kicker > span { width: 7px; height: 7px; border-radius: 50%; background: #c9a063; }
h1 { margin: 22px 0 18px; font-size: clamp(34px, 3.6vw, 51px); font-weight: 750; line-height: 1.4; letter-spacing: -1.5px; color: var(--ink); }
h1 > span { color: var(--forest); position: relative; white-space: nowrap; }
h1 > span::after { content: ''; position: absolute; bottom: -5px; left: 0; width: 100%; height: 8px; background: #dfca86; border-radius: 50%; opacity: .65; transform: rotate(-3deg); }
.top-banner p { color: var(--muted); font-size: 14px; line-height: 1.95; }
.hero-features { display: flex; flex-wrap: wrap; gap: 24px; margin-top: 24px; color: #52675d; font-size: 12px; }
.hero-features > span { display: flex; gap: 7px; align-items: center; }
.hero-features .anticon { color: var(--forest); font-size: 15px; }
.travel-illustration { position: relative; padding: 26px 18px 27px 0; }
.landscape-card { border: 9px solid #fffefb; border-radius: 10px; background: #fffefb; transform: rotate(3deg); box-shadow: 0 15px 40px #304b3612; overflow: hidden; }
.landscape-card svg { display: block; width: 100%; }
.landscape-caption { display: flex; justify-content: space-between; gap: 10px; padding: 17px 10px 9px; color: #506a59; font-size: 12px; }
.landscape-caption span:last-child { font-size: 9px; letter-spacing: 1px; }
.journey-stamp { position: absolute; z-index: 1; top: 0; right: -4px; width: 102px; height: 102px; display: flex; flex-direction: column; justify-content: center; text-align: center; border: 1px dashed #84946d; border-radius: 50%; background: #eef0dc; color: #4c6440; font-size: 17px; letter-spacing: 1px; transform: rotate(13deg); }
.journey-stamp span { margin-top: 5px; font-size: 8px; letter-spacing: 0; }
.journey-note { position: absolute; bottom: 0; left: -27px; display: flex; align-items: center; gap: 12px; padding: 16px 22px 16px 14px; background: #fffefb; border: 1px solid #e3e8df; border-radius: 12px; box-shadow: 0 10px 25px #304b3610; font-size: 13px; font-weight: 650; transform: rotate(-4deg); }
.note-icon { display: grid; place-items: center; width: 38px; height: 38px; background: #edf3e7; color: var(--forest); border-radius: 50%; font-size: 19px; }
.journey-note small { display: block; margin-top: 5px; font-size: 10px; font-weight: 400; color: var(--muted); }
.note-spark { color: #c09950; margin-left: 15px; font-size: 22px; }
.planning-steps { display: flex; align-items: center; justify-content: center; gap: 20px; margin: 10px 0 30px; color: #78847b; font-size: 12px; }
.planning-steps > span:not(.step-line) { display: flex; align-items: center; gap: 9px; }
.planning-steps b { display: grid; place-items: center; width: 26px; height: 26px; border: 1px solid #dce3d5; border-radius: 50%; font-size: 10px; font-weight: 500; }
.step-current { color: var(--forest); font-weight: 650; }
.step-current b { background: var(--forest); border-color: var(--forest); color: white; }
.step-line { width: 65px; height: 1px; background: #dce3d5; }
.form-card { border: 1px solid var(--line); border-radius: 20px; background: #fffefb; box-shadow: 0 8px 32px #304b3606; }
.form-card :deep(.ant-card-body) { padding: 36px 40px 14px; }
.form-card-header { display: flex; align-items: center; justify-content: space-between; gap: 20px; margin-bottom: 30px; padding-bottom: 28px; border-bottom: 1px solid var(--line); }
.form-eyebrow { font-size: 10px; color: #82957a; letter-spacing: 1.7px; font-weight: 650; }
h2 { margin: 8px 0 0; color: var(--ink); font-size: 23px; font-weight: 700; }
h2 > span { display: block; margin-top: 8px; color: var(--muted); font-size: 12px; font-weight: 400; }
.header-status { display: flex; flex-wrap: wrap; gap: 8px; justify-content: flex-end; }
.header-status span { padding: 6px 11px; border: 1px solid #e3e8df; border-radius: 6px; color: #65796b; font-size: 11px; }
.header-status span:first-child { background: #edf3e7; border-color: #edf3e7; color: var(--forest); }
.form-section { margin-bottom: 26px; padding-bottom: 8px; border-bottom: 1px solid #edf0e8; }
.form-section:last-of-type { border-bottom: 0; }
.section-header { display: flex; align-items: center; gap: 9px; margin-bottom: 22px; color: var(--forest); }
.section-number { margin-right: 4px; color: #8c9f7d; font-size: 12px; font-weight: 600; font-variant-numeric: tabular-nums; }
.section-header .anticon { font-size: 16px; }
.section-title { font-size: 15px; font-weight: 650; color: var(--ink); }
.form-label { color: #526359; font-size: 12px; font-weight: 500; }
.optional-label { margin-left: 6px; color: #8b968e; font-size: 11px; font-weight: 400; }
.form-card :deep(.ant-form-item-label) { padding-bottom: 8px; }
.form-card :deep(.ant-input), .form-card :deep(.ant-input-number), .form-card :deep(.ant-picker), .form-card :deep(.ant-select-selector) { background: #fdfefa; }
.form-card :deep(.ant-input-number-input) { height: 44px; }
.form-card :deep(.ant-input:hover), .form-card :deep(.ant-picker:hover), .form-card :deep(.ant-input-number:hover) { border-color: #7eaa93; }
.custom-textarea { padding: 14px; font-size: 13px; line-height: 1.9; resize: vertical; }
.city-suggestions { display: flex; align-items: center; gap: 9px; margin-top: 9px; flex-wrap: wrap; line-height: 1.7; }
.city-suggestions > span { color: #8a958c; font-size: 10px; }
.city-suggestions button { padding: 0 5px; background: transparent; border: 0; border-radius: 4px; color: #697f6c; cursor: pointer; font-size: 11px; }
.city-suggestions button:hover, .city-suggestions button[aria-pressed='true'] { color: var(--forest); background: #eaf2e4; }
.custom-checkbox-group { display: flex; flex-wrap: wrap; gap: 10px; }
.preference-tag { margin: 0; padding: 8px 12px; border: 1px solid #e4e8df; border-radius: 8px; background: #fffefb; font-size: 12px; transition: background .2s, border-color .2s; }
.preference-tag:hover { border-color: #88ac94; background: #f5f8f0; }
.preference-tag.ant-checkbox-wrapper-checked { color: var(--forest); border-color: #93b09a; background: #edf4e8; }
.preference-tag :deep(.ant-checkbox) { top: 0; }
.preference-tag :deep(.ant-checkbox-inner) { width: 13px; height: 13px; border-radius: 4px; }
.preference-tag :deep(.ant-checkbox-inner::after) { width: 4px; height: 7px; }
.preference-tag :deep(.ant-checkbox + span) { display: inline-flex; align-items: center; gap: 5px; padding-right: 0; }
.preference-icon { font-size: 14px; }
.submit-summary { display: flex; align-items: center; justify-content: space-between; gap: 15px; margin-bottom: 18px; color: #667d6a; font-size: 12px; }
.submit-summary i { font-style: normal; margin: 0 9px; color: #a7b19c; }
.submit-summary > span:last-child { color: #8a968d; font-size: 11px; }
.submit-button { display: flex; align-items: center; justify-content: center; gap: 10px; height: 54px; border: 0; border-radius: 11px; background: var(--forest); font-size: 15px; font-weight: 600; box-shadow: 0 5px 12px #176b5518; }
.submit-button:hover { background: #125640 !important; }
.submit-arrow { margin-left: 8px; font-size: 20px; font-weight: 400; }
.loading-container { padding: 18px 22px; border: 1px solid #d8e5d4; border-radius: 12px; background: #f4f8ee; text-align: center; }
.loading-status { margin: 12px 0 0; font-size: 12px; color: var(--forest); }
@media (max-width: 1000px) {
 .top-banner { gap: 38px; }
 .journey-note { left: -12px; }
 .form-card :deep(.ant-card-body) { padding: 28px 28px 10px; }
}
@media (max-width: 760px) {
 .home-container { padding: 26px 20px 40px; }
 .top-banner { grid-template-columns: 1fr; gap: 14px; margin-bottom: 28px; }
 .top-banner-content { text-align: center; }
 .banner-kicker, .hero-features { justify-content: center; }
 h1 { font-size: 38px; }
 .travel-illustration { width: min(380px, 90%); margin: 0 auto; }
 .planning-steps { gap: 9px; font-size: 10px; }
 .planning-steps > span:not(.step-line) { gap: 6px; }
 .step-line { width: 20px; }
 .form-card-header { align-items: flex-start; }
 .header-status { max-width: 110px; }
 .header-status span { padding: 4px 7px; }
 h2 { font-size: 20px; }
 .form-card :deep(.ant-card-body) { padding: 24px 20px 8px; }
 .form-section { margin-bottom: 20px; }
 .submit-summary { flex-wrap: wrap; gap: 7px; }
}
@media (max-width: 420px) {
 .planning-steps { display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 7px; font-size: 9px; }
 .planning-steps > span:not(.step-line) { flex-direction: column; text-align: center; }
 .planning-steps b { width: 20px; height: 20px; }
 .step-line { display: none; }
 .form-card-header { flex-direction: column; gap: 14px; }
 .header-status { max-width: none; }
 .preference-tag { padding: 8px; }
 .hero-features { gap: 16px; }
 .desktop-break { display: none; }
}
</style>
