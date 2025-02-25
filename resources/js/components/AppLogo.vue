<script setup lang="ts">
import AppLogoIcon from '@/components/AppLogoIcon.vue';
import { SIDEBAR_COOKIE_NAME, useSidebar } from './ui/sidebar/utils';
import { computed } from 'vue';

interface Props {
    class?: string;
}

defineProps<Props>();

const getSidebarState = (name: string) => {
    const value = `; ${document.cookie}`;
    const parts = value.split(`; ${name}=`);
    if (parts.length === 2) {
        return parts.pop()?.split(';').shift() ?? null; // Use optional chaining and nullish coalescing
    }
    return null; // Return null if the cookie is not found
};

const isSidebarCollapsed = computed(() => {
    return getSidebarState(SIDEBAR_COOKIE_NAME) === 'collapsed';
});

console.log(isSidebarCollapsed.value);
</script>

<template>
    <div class="flex  items-center justify-center rounded-md bg-sidebar-primary text-sidebar-primary-foreground"
        :class="{ '!min-w-8 !min-h-8 !-ml-2': !isSidebarCollapsed }">
        <AppLogoIcon class="!size-7 text-white dark:text-black" />
    </div>
    <div class="ml-1 grid flex-1 text-left text-sm">
        <span class="mb-0.5 truncate font-semibold leading-none">SOEKHA APP</span>
    </div>
</template>
