<template>
  <div class="fixed-powered">
    <span class="txt">Powered by</span>
    <span class="author">
      <a
        :href="GITHUB_REPO"
        target="_blank"
      >
        billd-live-admin
      </a>
    </span>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

import { GITHUB_REPO } from '@/constant';

export default defineComponent({
  components: {},
  setup() {
    return { GITHUB_REPO };
  },
});
</script>

<style lang="scss" scoped>
.fixed-powered {
  position: fixed;
  bottom: 0;
  width: 100%;
  height: 40px;
  border-radius: 10px;
  background-color: rgba(147, 115, 238, 0.04);
  color: #9373ee;
  text-align: center;
  line-height: 40px;

  user-select: none;
  .txt {
  }
  .author {
    margin-left: 10px;
    font-weight: bold;
    a {
      color: inherit;
      text-decoration: none;
    }
  }
}
</style>
