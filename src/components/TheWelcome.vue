<script setup>
import WelcomeItem from './WelcomeItem.vue'
import DocumentationIcon from './icons/IconDocumentation.vue'
import ToolingIcon from './icons/IconTooling.vue'
import EcosystemIcon from './icons/IconEcosystem.vue'
import CommunityIcon from './icons/IconCommunity.vue'
import SupportIcon from './icons/IconSupport.vue'
</script>

<template>
  <WelcomeItem>
    <template #icon>
      <DocumentationIcon />
    </template>
    <template #heading>민지는 개발을 공부해요</template>

    Vue라는걸 공부하기 시작했어요
    <a href="https://calendar.naver.com/main#%7B%22sSection%22%3A%22scheduleMain%22%2C%22oParameter%22%3A%7B%22sViewType%22%3A%22month%22%2C%22sDate%22%3A%222024-03-21%22%7D%7D" target="_blank" rel="noopener">바로 24년 3월 21일 오늘!</a>
    하루종일 엉뚱한 곳에 다운받고 다운받아서 하루를 날리고 과장님과 하윤언니의 도움으로 30분만에 성공했어요
  </WelcomeItem>

  <WelcomeItem>
    <template #icon>
      <ToolingIcon />
    </template>
    <template #heading>어떻게 했냐!</template>
    우선! 
    <a href="https://brew.sh/ko/" target="_blank" rel="noopener">homebrew</a>를 다운받고요, brew install npm을 해준 후 brew install nvm을 해줍니다<br>
    그 뒤에는 
    <a href="https://www.youtube.com/watch?v=G6rhxMuqnhU" target="_blank" rel="noopener">Vue 설치 영상</a> 보면서 셋팅했어요.
    <a href="https://github.com/johnsoncodehk/volar" target="_blank" rel="noopener">Volar</a>. If
    you need to test your components and web pages, check out
    <a href="https://www.cypress.io/" target="_blank" rel="noopener">Cypress</a> and
    <a href="https://on.cypress.io/component" target="_blank" rel="noopener"
      >Cypress Component Testing</a
    >.

    <br />

    다른 것들은 이런 md파일에서 확인 가능! <code>README.md</code>.
  </WelcomeItem>

  <WelcomeItem>
    <template #icon>
      <EcosystemIcon />
    </template>
    <template #heading>요즘 듣는 플리!</template>

    태버 플리랑 파묘 플리를 번갈아가면서 듣는 중!
    <a href="https://www.youtube.com/watch?v=ClapPEuOYTQ" target="_blank" rel="noopener">Tabber</a>,
    <a href="https://router.vuejs.org/" target="_blank" rel="noopener">Vue Router</a>,
    <a href="https://test-utils.vuejs.org/" target="_blank" rel="noopener">Vue Test Utils</a>, and
    <a href="https://github.com/vuejs/devtools" target="_blank" rel="noopener">Vue Dev Tools</a>. If
    you need more resources, we suggest paying
    <a href="https://github.com/vuejs/awesome-vue" target="_blank" rel="noopener">Awesome Vue</a>
    a visit.
  </WelcomeItem>

  <WelcomeItem>
    <template #icon>
      <CommunityIcon />
    </template>
    <template #heading>Community</template>

    Got stuck? Ask your question on
    <a href="https://chat.vuejs.org" target="_blank" rel="noopener">Vue Land</a>, our official
    Discord server, or
    <a href="https://stackoverflow.com/questions/tagged/vue.js" target="_blank" rel="noopener"
      >StackOverflow</a
    >. You should also subscribe to
    <a href="https://news.vuejs.org" target="_blank" rel="noopener">our mailing list</a> and follow
    the official
    <a href="https://twitter.com/vuejs" target="_blank" rel="noopener">@vuejs</a>
    twitter account for latest news in the Vue world.
  </WelcomeItem>

  <WelcomeItem>
    <template #icon>
      <SupportIcon />
    </template>
    <template #heading>Support Vue</template>

    As an independent project, Vue relies on community backing for its sustainability. You can help
    us by
    <a href="https://vuejs.org/sponsor/" target="_blank" rel="noopener">becoming a sponsor</a>.
  </WelcomeItem>
</template>
