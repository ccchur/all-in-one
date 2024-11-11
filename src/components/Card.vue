<template>
  <div class="card">
    <div class="card-header">
      <a-avatar :size="88" class="avatar">
        <img alt="avatar" :src="props.userInfo!.avatar" />
      </a-avatar>
      <h2 class="username">@{{ props.userInfo!.name }}</h2>
      <p class="bio">{{ props.userInfo!.description }}</p>
    </div>
    <div class="card-body">
      <div class="link-list" v-for="item in props.userInfo!.link">
        <a href="#" class="link-item">
          <!-- <img class="link-icon" alt="link-icon"
            :src="item.icon" /> -->
          <span class="link-icon">
            {{ item.name }}
          </span>
          <div class="content">
            <span class="link-title">{{ item.url }}</span>
            <icon-right class="arrow-icon" />
          </div>
        </a>
      </div>
    </div>
    <div class="card-footer">
      <p class="footer-text">© 2024 张三的链接树 | Made with ❤️</p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { defineProps } from 'vue';

interface LinkItem {
  id: number;
  icon: string;
  text: string;
  link: string;
}

const props = defineProps({
  userInfo: {
    type: Object
  }
})


console.log('🟢🟢🟢',props);
</script>
<style scoped>
  .card {
    width: 33%;
    max-width: 600px;
    margin: 0 auto;
    padding: 2rem;
    border-radius: 24px;
    border: 1px solid rgba(229, 229, 229, 0.8);
    box-shadow: 0 8px 24px rgba(0, 0, 0, 0.08);
    text-align: center;
    background: #fff;
    transition: all 0.3s ease;
  }

  .card:hover {
    transform: translateY(-5px);
    box-shadow: 0 12px 36px rgba(0, 0, 0, 0.12);
  }

  .card-header {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-bottom: 2rem;
  }

  .avatar {
    border: 4px solid #fff;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    transition: transform 0.3s ease;
  }

  .avatar:hover {
    transform: scale(1.05);
  }

  .username {
    margin: 1rem 0 0.8rem;
    font-size: 1.6rem;
    font-weight: 700;
    background: linear-gradient(45deg, #2196f3, #4caf50);
    background-clip: text;
    -webkit-text-fill-color: transparent;
  }

  .bio {
    color: #666;
    margin: 0;
    font-size: 1rem;
    line-height: 1.5;
  }

  .link-list {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }

  .link-item {
    display: flex;
    align-items: center;
    padding: 1rem;
    background: #f8f9fa;
    border-radius: 12px;
    text-decoration: none;
    color: #333;
    transition: all 0.3s ease;
    border: 1px solid transparent;
    margin-top: 10px;
  }

  .link-item:hover {
    background: #fff;
    transform: translateY(-2px);
    border-color: #e0e0e0;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
  }

  .link-title {
    font-weight: 600;
    font-size: 1rem;
  }

  .link-icon {
    width: 24px;
    height: 24px;
    margin-right: 12px;
    border-radius: 6px;
  }

  .content {
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .arrow-icon {
    color: #666;
    transition: transform 0.3s ease;
    font-size: 16px;
  }

  .link-item:hover .arrow-icon {
    transform: translateX(4px);
    color: #2196f3;
  }

  .card-footer {
    margin-top: 2rem;
    padding-top: 1.5rem;
    border-top: 1px solid #eee;
  }

  .footer-text {
    color: #888;
    font-size: 0.875rem;
    margin: 0;
  }
</style>