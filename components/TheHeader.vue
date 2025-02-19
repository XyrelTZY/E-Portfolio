<template>
  <header
    class="sticky z-20 top-0 duration-200 px-4 border-b border-solid"
    :class="{
      'py-4 dark:bg-black bg-slate-200 border-primary border-b-2': y > 0,
      'py-6 bg-transparent border-transparent': y <= 0,
    }"
  >
    <nav
      class="flex flex-row items-center justify-between max-w-[1400px] mx-auto"
    >
      <div
        class="flex gap-4 items-center cursor-pointer text-primary hover:text-blue-300"
        @click="goTop"
      >
        <span class="inline-block">
          <img
            src="../assets/images/SchoolLogo.png"
            alt="School Logo"
            class="h-12 w-12"
          />
        </span>
        <h1 class="font-medium text-xl">
          <b class="font-bold poppins mr-1">
            E
            <span class="font-bold poppins mr-1inline-block">-</span>
          </b>
          <span class="font-bold poppins md:inline-block"> Portfolio </span>
        </h1>
      </div>

      <div
        class="flex gap-4 items-center ml-auto relative"
        v-motion-fade-visible-once
      >
        <ThemeToggler />
        <button
          aria-label="expand mobile menu button"
          @click="isOpen = !isOpen"
          class="md:hidden block p-2 absolute top-0 right-0"
          :class="{
            open: isOpen,
            'focus:outline-none': true,
          }"
        >
          <span class="hamburger-top"></span>
          <span class="hamburger-middle"></span>
          <span class="hamburger-bottom"></span>
        </button>
      </div>

      <nav class="items-center flex-row hidden md:flex">
        <div class="flex pr-3">
          <div class="sm:flex items-center gap-4 text-center hidden">
            <a
              class="hover:text-primary hover:underline"
              v-for="link in NAV_LINKS"
              :href="link.href"
              :key="link.href"
            >
              {{ link.label }}
            </a>
          </div>
        </div>
      </nav>
    </nav>

    <nav
      v-show="isOpen"
      @click="isOpen = false"
      class="md:hidden p-4 mt-2 flex flex-col gap-2 text-center font-bold"
      :class="{
        'py-4 dark:bg-slate-950 bg-slate-200 border-primary dark:border-green-950':
          y > 0,
        'py-6 bg-transparent border-transparent': y <= 0,
      }"
    >
      <a
        class="border rounded p-2 border-primary animate-link"
        v-for="link in NAV_LINKS"
        :href="link.href"
        :key="link.href"
      >
        {{ link.label }}
      </a>
      <!-- <NuxtLink
        to="/about"
        class="border rounded p-2 border-primary animate-link"
        >Preface</NuxtLink
      > -->
    </nav>
  </header>
</template>

<script setup lang="ts">
import { NAV_LINKS } from "@/data/constants";

defineProps<{
  y: number;
  goTop: () => void;
}>();

const isOpen = ref(false);
</script>
