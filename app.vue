<template>
  <div>
    <!-- <NuxtPage /> -->
    <nav>
      <ContentNavigation v-slot="{ navigation }">
        <ul>
          <li v-for="link of navigation" :key="link._path">
            <NuxtLink :to="link._path">
              {{ link.title }}
            </NuxtLink>
          </li>
        </ul>
      </ContentNavigation>
    </nav>

    <main>
      <ContentDoc path="/breeze" />
      <br />
      <br />
      <br />
      <ContentDoc path="/something" />
      <br />
      <ContentRenderer :value="data" />
      <ContentList v-slot="{ list }" path="/something">
        <div v-for="article in list" :key="article._path">
          {{ article }}
          <!-- <h2>{{ article.title }}</h2> -->
          <!-- <p>{{ article.description }}</p> -->
        </div>
      </ContentList>
    </main>
  </div>
</template>

<script setup lang="ts">
const { data } = await useAsyncData('get-document', () => queryContent('/something').findOne())
</script>
