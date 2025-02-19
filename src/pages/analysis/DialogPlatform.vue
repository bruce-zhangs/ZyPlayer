<template>
  <div class="platform-container">
    <div class="support-title">
      <span class="support-separator"></span>
      <p class="support-tip">
        <t-link theme="default" hover="color">
          <template #suffixIcon>
            <jump-icon style="align-items: center; display: inherit" />
          </template>
          支持平台
        </t-link>
      </p>
    </div>
    <div class="support-platform">
      <div v-for="(item, index) in VIDEOSITES" :key="index" class="logo-item" @click="openPlatform(item)">
        <div v-if="item.show" class="logo" v-html="item.img"></div>
      </div>
    </div>
  </div>
</template>
<script setup lang="ts">
import _ from 'lodash';
import { JumpIcon } from 'tdesign-icons-vue-next';
import { reactive, ref, watch } from 'vue';

import PLATFORM_CONFIG from '@/config/platform';

const props = defineProps({
  visible: {
    type: Boolean,
    default: false,
  },
});

const formVisible = ref(false); // 控制dialog

const emit = defineEmits(['update:visible', 'open-platform']);

const VIDEOSITES = reactive({
  ...PLATFORM_CONFIG.site,
}); // 视频网站列表

watch(
  () => formVisible.value,
  (val) => {
    emit('update:visible', val);
  },
);
watch(
  () => props.visible,
  (val) => {
    formVisible.value = val;
  },
);

const openPlatform = (item) => {
  emit('open-platform', { ...item });
};
</script>

<style lang="less" scoped>
@import '@/style/variables.less';
@import '@/style/index.less';

.platform-container {
  .support-title {
    margin: 5px 0;
    .support-separator {
      border: 0.1rem solid var(--td-brand-color);
      height: 0.6rem;
      border-radius: var(--td-radius-default);
      display: inline-block;
    }
    .support-tip {
      margin-left: 5px;
      display: inline-block;
      text-align: left;
      a {
        font-weight: 500;
      }
    }
  }
  .support-platform {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: flex-start;
  }
  .logo-item {
    cursor: pointer;
    margin-right: 8px;
    padding: var(--td-comp-paddingTB-s) var(--td-comp-paddingLR-s) var(--td-comp-paddingTB-m);
    border-radius: var(--td-radius-medium);
    background-color: var(--td-bg-input);
    &:hover {
      background-color: var(--td-bg-color-component-hover);
    }

    .logo {
      width: 70px;
      height: 15px;
    }
  }
}
</style>
