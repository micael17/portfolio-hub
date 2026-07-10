<template>
  <div class="app-wrap">
    <div class="border-outer">
      <div class="border-inner">
        <div class="hero">
          <p class="vertical-text title">혼 례</p>
          <div class="hero-image"></div>
        </div>
        
        <div class="content">
          <div class="ornament"></div>
          <p class="greeting">
            두 사람이 만나 하나의 매듭을 맺습니다.<br>
            귀한 걸음 하시어 축복해 주시면<br>
            더없는 기쁨으로 간직하겠습니다.
          </p>

          <div class="names">
            <p>이서준 &middot; 한지민</p>
          </div>

          <div class="info-grid">
            <div class="info-cell">
              <strong>일시</strong>
              <p>이천이십육년 시월 이십사일<br>토요일 오후 한 시</p>
            </div>
            <div class="info-cell">
              <strong>장소</strong>
              <p>삼청각 일화당<br>서울특별시 성북구 대사관로 3</p>
            </div>
          </div>

          <button class="btn">참석 여부 알림</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
useHead({ title: 'Hanok Wedding' })
definePageMeta({ layout: false })
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Noto+Serif+KR:wght@300;400;600;900&display=swap');

.app-wrap {
  background: #f4ede1;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 1rem;
}

.border-outer {
  max-width: 450px;
  width: 100%;
  background: #fff;
  border: 10px solid #8e2b24;
  padding: 5px;
}

.border-inner {
  border: 1px solid #8e2b24;
  padding: 2rem;
  background: #fff9f0;
}

.hero {
  display: flex;
  justify-content: space-between;
  margin-bottom: 3rem;
  border-bottom: 2px solid #8e2b24;
  padding-bottom: 2rem;
}

.vertical-text {
  writing-mode: vertical-rl;
  font-family: 'Noto Serif KR', serif;
}

.title {
  font-size: 3rem;
  font-weight: 900;
  color: #8e2b24;
  letter-spacing: 2rem;
  margin-top: 2rem;
}

.hero-image {
  width: 70%;
  height: 300px;
  background: url('https://images.unsplash.com/photo-1582560469795-09c31fa759be?w=600&q=80') center/cover;
  border: 1px solid #8e2b24;
}

.content {
  text-align: center;
  font-family: 'Noto Serif KR', serif;
}

.ornament {
  width: 30px;
  height: 30px;
  background: #113255;
  margin: 0 auto 2rem;
  transform: rotate(45deg);
}

.greeting {
  line-height: 2.2;
  font-size: 1.1rem;
  color: #333;
  margin-bottom: 3rem;
}

.names {
  font-size: 1.5rem;
  font-weight: 600;
  color: #8e2b24;
  margin-bottom: 3rem;
}

.info-grid {
  border-top: 1px solid #8e2b24;
  border-bottom: 1px solid #8e2b24;
}

.info-cell {
  padding: 1.5rem 0;
  border-bottom: 1px dashed #d5c8b5;
}

.info-cell:last-child {
  border-bottom: none;
}

.info-cell strong {
  display: block;
  font-size: 0.9rem;
  color: #8e2b24;
  margin-bottom: 0.5rem;
}

.info-cell p {
  line-height: 1.6;
  font-size: 1.05rem;
}

.btn {
  margin-top: 3rem;
  width: 100%;
  background: #113255;
  color: #fff;
  border: none;
  padding: 1.2rem;
  font-family: 'Noto Serif KR', serif;
  font-size: 1.1rem;
  cursor: pointer;
  letter-spacing: 2px;
}
</style>
