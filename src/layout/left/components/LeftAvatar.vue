<template>
  <n-popover
    v-model:show="infoShow"
    :placement="shrinkStatus ? 'bottom-start' : 'right-start'"
    :show-arrow="false"
    style="padding: 0; background: rgba(255, 255, 255, 0.2); backdrop-filter: blur(10px)"
    trigger="click">
    <template #trigger>
      <!-- 头像 -->
      <div class="relative size-34px rounded-50% cursor-pointer">
        <n-avatar :color="'#909090'" :size="34" :src="avatarSrc" fallback-src="/logo.png" round />

        <div
          class="bg-[--left-bg-color] text-10px rounded-50% size-12px absolute bottom--2px right--2px border-(2px solid [--left-bg-color])"
          @click.stop="openContent('在线状态', 'onlineStatus', 320, 480)">
          <img :src="currentState?.url" alt="" class="rounded-50% size-full" />
        </div>
      </div>
    </template>
    <!-- 用户个人信息框 -->
    <n-flex
      :size="26"
      :style="`background: linear-gradient(to bottom, ${currentState?.bgColor} 0%, ${themeColor} 100%)`"
      class="size-full p-15px box-border rounded-8px"
      vertical>
      <!-- 头像以及信息区域 -->
      <n-flex :size="25" align="center" justify="space-between" class="select-none cursor-default">
        <n-flex>
          <n-avatar
            :color="'#909090'"
            :src="avatarSrc"
            round
            fallback-src="/logo.png"
            class="size-68px text-20px select-none cursor-default" />

          <n-flex :size="10" class="text-[--text-color]" justify="center" vertical>
            <span class="text-18px">{{ userStore.userInfo.name }}</span>
            <span class="text-(12px [--info-text-color])">账号 {{ userStore.userInfo.account }}</span>
            <n-flex
              :size="5"
              align="center"
              class="item-hover ml--4px"
              @click="openContent('在线状态', 'onlineStatus', 320, 480)">
              <img :src="currentState?.url" alt="" class="rounded-50% size-18px" />
              <span>{{ currentState?.title }}</span>
            </n-flex>
          </n-flex>
        </n-flex>

        <n-flex :size="5" align="center" class="item-hover" vertical>
          <svg class="size-20px"><use href="#thumbs-up"></use></svg>
          <span class="text-12px">9999+</span>
        </n-flex>
      </n-flex>
      <!-- 地址 -->
      <n-flex :size="26" class="select-none">
        <span class="text-[--info-text-color]">所在地</span>
        <span>中国</span>
      </n-flex>
      <!-- 动态 -->
      <n-flex :size="40" class="select-none">
        <span class="text-[--info-text-color]">动态</span>
        <n-image-group>
          <n-flex :class="shrinkStatus ? 'overflow-hidden w-180px' : ''" :size="6" :wrap="false">
            <n-image
              v-for="n in 4"
              :key="n"
              class="rounded-8px"
              preview-disabled
              src="https://07akioni.oss-cn-beijing.aliyuncs.com/07akioni.jpeg"
              width="50" />
          </n-flex>
        </n-image-group>
      </n-flex>

      <n-flex :size="40" align="center" justify="center">
        <n-button secondary @click="handleEditing"> 编辑资料 </n-button>
      </n-flex>
    </n-flex>
  </n-popover>
</template>
<script setup lang="ts">
import { leftHook } from '../hook.ts'
import { useUserStore } from '@/stores/user.ts'
import { AvatarUtils } from '~/src/utils/AvatarUtils.ts'

const userStore = useUserStore()
const avatarSrc = computed(() => AvatarUtils.getAvatarUrl(userStore.userInfo.avatar as string))
const { shrinkStatus, currentState, infoShow, themeColor, openContent, handleEditing } = leftHook()
</script>
<style lang="scss" scoped>
@use '../style';
</style>
