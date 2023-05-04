<template>
  <div class="flex-shrink-0 p-3">
  <a href="/" class="d-flex align-items-center pb-3 mb-3 text-decoration-none border-bottom">
    <span class="fs-5 fw-semibold">BootstrapVueNext</span>
  </a>
  <BNavbarNav>
    <BNav>
      <BNavItem to="/introduction/index">Introduction</BNavItem>
      <BCollapse :modelValue="actualPage == 'introduction'" class="small pb-1 px-2" >
        <BNavItem to="/introduction/index">Introduction</BNavItem>
        <BNavItem to="/introduction/getting-started">Getting Started</BNavItem>
      </BCollapse>
      <BNavItem to="/reference/components" >Components</BNavItem>
      <BCollapse :modelValue="actualPage == 'components'" class="small pb-1 px-2" >
        <BNavItem to="#">Alert</BNavItem>
        <BNavItem to="#">Aspect</BNavItem>
      </BCollapse>
      <BNavItem to="/reference/composables">Composables</BNavItem>
      <BCollapse :modelValue="actualPage == 'composables'" class="small pb-1 px-2" >
        <BNavItem to="#">Alert</BNavItem>
        <BNavItem to="#">Aspect</BNavItem>
      </BCollapse>
      <BNavItem to="/reference/directives">Directives</BNavItem>
      <BCollapse :modelValue="actualPage == 'directives'" class="small pb-1 px-2" >
        <BNavbarNav>
          <BNav>
              <BNavItem to="#">Hover</BNavItem>
              <BNavItem to="#">Popover</BNavItem>
          </BNav>
        </BNavbarNav>
      </BCollapse>
    </BNav>
    <BNav>
      <BNavItem to="/reference/icons">Icons</BNavItem>
    </BNav>
    <BNav>
      <BNavItem to="/reference/types">Types</BNavItem>
    </BNav>
    <BNav>
      <BNavItem to="/migration-guide">Migrate</BNavItem>
    </BNav>
  </BNavbarNav>
</div>
</template>
<script setup lang="ts">
import { useData, onContentUpdated } from 'vitepress';
import { ref } from 'vue';

const { page } = useData();
const actualPage = ref('home')

onContentUpdated(() => {
  actualPage.value = getActualPage();
});

function getActualPage() {
  console.log(page.value.filePath);
  if(page.value.filePath.includes('introduction')) return 'introduction'
  else if(page.value.filePath.includes('/components')) return 'components'
  else if(page.value.filePath.includes('/composables')) return 'composables'
  else if(page.value.filePath.includes('/directives')) return 'directives'
  else if(page.value.filePath.includes('/icons')) return 'icons'
  else if(page.value.filePath.includes('migration-guide')) return 'migration'
  else return 'types';
}


</script>