<template>
  <header class="header-warp">
    <div class="left">
      <BreadcrumbCpt></BreadcrumbCpt>
    </div>
    <div class="action">
      <div
        class="lang"
        @click="handleClick"
      >
        <n-icon size="20">
          <language></language>
        </n-icon>
      </div>
      <n-dropdown
        trigger="hover"
        :options="options"
        @select="handleSelect"
      >
        <div class="user">
          <img
            class="avatar"
            :src="userInfo?.avatar"
            alt=""
          />
          <span class="name">{{ userInfo?.username }}</span>
        </div>
      </n-dropdown>
      <div
        class="setting"
        @click="handleClick"
      >
        <n-icon size="20">
          <SettingsOutline></SettingsOutline>
        </n-icon>
      </div>
    </div>
  </header>
</template>

<script lang="ts" setup>
import { Language, SettingsOutline } from '@vicons/ionicons5';
import { windowReload } from 'billd-utils';
import { ref } from 'vue';
import { useRouter } from 'vue-router';

import BreadcrumbCpt from '@/components/Breadcrumb/index.vue';
import { BLOG_CLIENT_URL } from '@/constant';
import { useAppStore } from '@/store/app';
import { useUserStore } from '@/store/user';

const userStore = useUserStore();
const appStore = useAppStore();
const router = useRouter();

const options = ref([
  {
    label: '博客前台',
    key: '1',
  },
  {
    label: '账号设置',
    key: '2',
  },
  {
    label: '退出登录',
    key: '3',
  },
]);

const handleSelect = (v) => {
  if (v === '1') {
    window.open(BLOG_CLIENT_URL);
  } else if (v === '2') {
    router.push('/setting/account').then(
      () => {},
      () => {}
    );
  } else if (v === '3') {
    userStore.logout();
    appStore.setRoutes([]);
    router.push('/login').then(
      () => {
        windowReload();
      },
      (err) => {
        console.log(err);
      }
    );
  }
};

function handleClick() {
  window.$message.info('敬请期待!');
}
const userInfo = userStore.userInfo;
</script>

<style lang="scss" scoped>
.header-warp {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 48px;
  border-bottom: 1px solid #eee;
  .left {
    padding: 0 10px;
  }
  .action {
    display: flex;
    align-items: center;
    min-width: 150px;
    > div:hover {
      cursor: pointer;
      background-color: #f6f6f6;
    }
    .user {
      display: flex;
      align-items: center;
      padding: 0 10px;
      height: 48px;
      .avatar {
        width: 20px;
        height: 20px;
        border-radius: 50%;
      }
      .name {
        margin-left: 6px;
        font-size: 14px;
      }
    }
    .lang,
    .setting {
      display: inline-flex;
      height: 48px;
      align-items: center;
      padding: 0 10px;
    }
  }
}
</style>
