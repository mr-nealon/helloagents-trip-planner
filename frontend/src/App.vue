<template>
  <a-config-provider :theme="theme">
    <a-layout class="app-layout">
      <a-layout-header class="app-header">
        <div class="header-inner">
          <router-link to="/" class="app-brand" aria-label="HelloAgents 旅行规划首页">
            <span class="brand-mark"><CompassOutlined /></span>
            <span class="brand-title">HelloAgents <small>旅行助手</small></span>
          </router-link>
          <div class="header-right">
            <span class="header-caption">每一次出发，都值得好好计划</span>
            <router-link to="/" class="header-link">规划旅程 <ArrowUpOutlined /></router-link>
          </div>
        </div>
      </a-layout-header>
      <a-layout-content id="main-content" class="app-content"><router-view /></a-layout-content>
      <a-layout-footer class="app-footer">
        <span>HelloAgents <span class="footer-dot">·</span> 让期待，成为行程</span>
        <span>用心规划，自在出发 ©2026</span>
      </a-layout-footer>
    </a-layout>
  </a-config-provider>
</template>

<script setup lang="ts">
import { ArrowUpOutlined, CompassOutlined } from '@ant-design/icons-vue'
const theme = {
  token: {
    colorPrimary: '#176b55', colorInfo: '#176b55', colorText: '#263d35',
    colorTextSecondary: '#728078', colorBorder: '#dce3da', borderRadius: 10,
    fontFamily: "'Segoe UI', 'PingFang SC', 'Microsoft YaHei', sans-serif",
    controlHeightLG: 46
  }
}
</script>

<style>
:root { --forest: #176b55; --ink: #263d35; --muted: #728078; --paper: #f7f8f2; --line: #e3e8df; }
* { box-sizing: border-box; }
html { scroll-behavior: smooth; scroll-padding-top: 30px; }
body { margin: 0; color: var(--ink); background: var(--paper); }
::selection { background: #d9e9ce; color: #173f31; }
a, button, input, textarea { -webkit-tap-highlight-color: transparent; }
:focus-visible { outline: 3px solid #8fbba8; outline-offset: 4px; }
.app-layout { min-height: 100vh; background: var(--paper); font-family: 'Segoe UI', 'PingFang SC', 'Microsoft YaHei', sans-serif; }
.app-layout .app-header { height: 80px; padding: 0 40px; background: #fffefb; border-bottom: 1px solid var(--line); line-height: normal; }
.header-inner { max-width: 1240px; height: 100%; margin: auto; display: flex; justify-content: space-between; align-items: center; gap: 20px; }
.app-header .app-brand { display: inline-flex; flex-direction: row; align-items: center; flex-shrink: 0; gap: 12px; color: var(--ink); font-size: 21px; font-weight: 750; letter-spacing: -.5px; line-height: 1; white-space: nowrap; }
.app-brand:hover { color: var(--forest); }
.app-brand .brand-title { display: inline-flex; align-items: center; gap: 9px; line-height: 1.2; }
.app-brand small { display: inline; margin: 0; color: var(--muted); font-size: 13px; font-weight: 500; letter-spacing: 1px; }
.app-brand .brand-mark { flex: 0 0 43px; width: 43px; height: 43px; display: inline-flex; align-items: center; justify-content: center; color: white; background: var(--forest); border-radius: 14px 14px 14px 3px; font-size: 26px; line-height: 1; }
.header-right { display: flex; align-items: center; gap: 32px; }
.header-caption { color: var(--muted); font-size: 12px; }
.header-link { display: flex; align-items: center; gap: 14px; color: var(--forest); font-size: 13px; font-weight: 650; }
.header-link .anticon { transform: rotate(45deg); }
.app-content { padding: 0; }
.app-footer { max-width: 1240px; width: calc(100% - 80px); margin: 0 auto; padding: 25px 0; display: flex; justify-content: space-between; gap: 12px; border-top: 1px solid var(--line); background: transparent; color: var(--muted); font-size: 12px; }
.footer-dot { padding: 0 9px; color: var(--forest); }
@media (max-width: 640px) {
  .app-layout .app-header { height: 70px; padding: 0 20px; }
  .app-header .app-brand { font-size: 18px; gap: 9px; }
  .header-caption { display: none; }
  .app-footer { width: calc(100% - 40px); flex-direction: column; font-size: 11px; }
}
@media (max-width: 480px) {
  .header-inner { gap: 10px; }
  .app-header .app-brand { font-size: 16px; }
  .app-brand .brand-mark { flex-basis: 34px; width: 34px; height: 34px; font-size: 22px; border-radius: 11px 11px 11px 3px; }
  .app-brand .brand-title { gap: 6px; }
  .app-brand small { font-size: 11px; letter-spacing: 0; }
  .header-link { font-size: 11px; }
  .header-link .anticon { display: none; }
}
@media (prefers-reduced-motion: reduce) {
  html { scroll-behavior: auto; }
  *, *::before, *::after { animation-duration: .01ms !important; transition-duration: .01ms !important; }
}
</style>
