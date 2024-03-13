<template>
  <main class="min-h-screen">
    <AppHeader class="mb-8" title="Bookmarks" :description="description" />
    <ul class="space-y-2">
      <li v-for="bookmark in bookmarks" :key="bookmark.id">
        <a
          :href="bookmark.url"
          target="_blank"
          class="flex items-center gap-3 hover:bg-gray-100 dark:hover:bg-white/10 p-2 rounded-lg -m-2 text-sm min-w-0"
        >
          <UAvatar
            :src="getThumbnail(bookmark.url)"
            :alt="bookmark.label"
            :ui="{ rounded: 'rounded-md' }"
          />
          <p class="truncate text-gray-700 dark:text-gray-200">
            {{ bookmark.label }}
          </p>
          <span class="flex-1"></span>
          <span class="text-xs font-medium text-gray-400 dark:text-gray-600">
            {{ getHost(bookmark.url) }}
          </span>
        </a>
      </li>
    </ul>
  </main>
</template>

<script setup>
const description =
  "Awesome things I've found on the internet. This page is still needs a lot more work but I'll add more later.";
useSeoMeta({
  title: "Bookmarks | Noah Victoriano",
  description,
});

const bookmarks = [
  {
    id: 1,
    label: "Structure and Interpretation of Computer Programs",
    url: "https://sarabander.github.io/sicp/html/index.xhtml",
  },
  {
    id: 2,
    label: "The Last Algorithms Course You'll Need",
    url: "https://frontendmasters.com/courses/algorithms/big-o-time-complexity/",
  },
  {
    id: 3,
    label: "Learn Go with Tests",
    url: "https://quii.gitbook.io/learn-go-with-tests/",
  },
];

function getHost(url) {
  const parsedUrl = new URL(url);
  let host = parsedUrl.host;
  if (host.startsWith("www.")) {
    host = host.substring(4);
  }
  return host;
}

function getThumbnail(url) {
  const host = getHost(url);
  return `https://logo.clearbit.com/${host}`;
}
</script>
