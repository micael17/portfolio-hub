<template>
  <NuxtLink :to="to" class="admin-demo-link" aria-label="관리자 데모 열기">
    <span class="admin-demo-icon">⌘</span>
    <span><small>STORE OWNER</small><strong>Admin Demo</strong></span>
    <i>↗</i>
  </NuxtLink>
</template>

<script setup>
defineProps({ to: { type: String, required: true } })
</script>

<style scoped>
.admin-demo-link {
  position: fixed;
  z-index: 18;
  right: 22px;
  bottom: 22px;
  min-width: 174px;
  padding: 10px 12px;
  display: grid;
  grid-template-columns: 34px 1fr auto;
  align-items: center;
  gap: 9px;
  border: 1px solid rgba(255, 255, 255, 0.18);
  border-radius: 10px;
  background: rgba(20, 21, 20, 0.94);
  color: #fff;
  box-shadow: 0 10px 32px rgba(0, 0, 0, 0.22);
  text-decoration: none;
  backdrop-filter: blur(12px);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.admin-demo-link:hover {
  transform: translateY(-3px);
  box-shadow: 0 14px 38px rgba(0, 0, 0, 0.28);
}

.admin-demo-icon {
  width: 34px;
  height: 34px;
  display: grid;
  place-items: center;
  border-radius: 7px;
  background: #fff;
  color: #171817;
  font: 600 13px/1 Arial, sans-serif;
}

.admin-demo-link > span:nth-child(2) {
  display: flex;
  flex-direction: column;
  line-height: 1.15;
}

.admin-demo-link small {
  margin-bottom: 4px;
  color: #aeb0ae;
  font: 500 7px/1 Arial, sans-serif;
  letter-spacing: 1.2px;
}

.admin-demo-link strong {
  color: #fff;
  font: 600 12px/1 Arial, sans-serif;
  letter-spacing: 0;
  text-transform: none;
}

.admin-demo-link i {
  color: #bfc1bf;
  font: normal 12px/1 Arial, sans-serif;
}

@media (max-width: 640px) {
  .admin-demo-link {
    right: 12px;
    bottom: 12px;
    min-width: 0;
    grid-template-columns: 30px auto;
    padding: 8px 11px 8px 8px;
  }

  .admin-demo-icon {
    width: 30px;
    height: 30px;
  }

  .admin-demo-link small,
  .admin-demo-link i {
    display: none;
  }
}
</style>
