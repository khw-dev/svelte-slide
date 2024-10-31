<script lang="ts">
  import { onMount } from 'svelte';

  let currentIndex: number = 0;
  let totalSlides: number = 11;

  const slideWidth = window.innerWidth;

  function scrollToSlide(index: number) {
    const container = document.getElementById('slideContainer');
    if (container) {
      container.style.transform = `translateX(-${index * slideWidth}px)`;
    }
    updateProgressBar();
  }

  function nextSlide() {
    if (currentIndex < totalSlides - 1) {
      currentIndex++;
      scrollToSlide(currentIndex);
    }
  }

  function previousSlide() {
    if (currentIndex > 0) {
      currentIndex--;
      scrollToSlide(currentIndex);
    }
  }

  function handleKeydown(event: KeyboardEvent) {
    if (event.key === 'ArrowRight') {
      nextSlide();
    } else if (event.key === 'ArrowLeft') {
      previousSlide();
    }
  }

  function updateProgressBar() {
    const progressBar = document.getElementById('progressBar');
    if (progressBar) {
      const progress = ((currentIndex + 1) / totalSlides) * 100;
      progressBar.style.width = `${progress}%`;
    }
  }

  onMount(() => {
    window.addEventListener('keydown', handleKeydown);
    updateProgressBar();

    return () => {
      window.removeEventListener('keydown', handleKeydown);
    };
  });
</script>

<style>
  :root {
    --bg-color: #fff;
    --slide-width: 11;
  }

  #slideContainer {
    display: flex;
    transition: transform 0.5s ease-in-out;
    width: calc(var(--slide-width) * 100vw);
    overflow: hidden;
  }

  .slide {
    width: 100vw;
    height: 100vh;
    flex-shrink: 0;
    background-color: var(--bg-color, #fff);
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
    flex-direction: column;
    gap: 20px;
  }

  .slide h1, .slide p {
    margin: 0;
  }

  .slide:first-child h1 {
    font-size: 5rem;
    margin-bottom: 0;
  }

  .title {
    font-size: 3.5rem;
  }

  .subtitle {
    font-size: 1.5rem;
    text-align: center;
  }

  .subtitle.left {
    text-align: left;
  }

  .subtitle.right {
    text-align: right;
  }

  .source {
    font-size: 1rem;
    color: blue;
  }

  .source:hover {
    text-decoration: underline;
  }

  .progress-bar {
    position: fixed;
    bottom: 0;
    left: 0;
    height: 5px;
    background-color: #4863e8;
    width: 0%;
    transition: width 0.2s;
    z-index: 100;
  }
</style>

<div id="slideContainer">
  <div class="slide">
      <h1 class="title">Open Source</h1>
      <p class="subtitle">오픈 소스와 라이선스</p>
  </div>
  <div class="slide">
    <h1 class="title">오픈 소스란?</h1>
    <p class="subtitle">
      오픈 소스 소프트웨어는 개방형 협업을 통해 개발되고 유지 관리되는 소프트웨어이다.
      <br>일반적으로 누구나 무료로 사용, 변경 및 재배포 할 수 있다.
      <a href="https://www.ibm.com/kr-ko/topics/open-source" target="_blank" class="source">[1]</a>
    </p>
  </div>
  <div class="slide">
    <h1 class="title">라이선스란?</h1>
    <p class="subtitle">
      라이선스는 소프트웨어의 사용 조건을 규정하는 계약이다.
      <br>오픈 소스 라이선스는 소프트웨어의 자유로운 사용을 보장하면서도 저작권을 보호한다.
      <a href="https://www.copyright.or.kr/information-materials/dictionary/view.do?glossaryNo=80&pageIndex=1&clscode=01&amp;searchText=&amp;searchkeyword=%EB%9D%BC%EC%9D%B4%EC%84%A0%EC%8A%A4&amp;searchIdx=&amp;pageDisplaySize=10&amp;searchLangType=&amp;searchTarget=" target="_blank" class="source">[2]</a>
      <br>
      (ex, MIT, Apache, GPL, BSD 등)
    </p>
  </div>
  <div class="slide">
    <h1 class="title">오픈 소스의 장점</h1>
    <p class="subtitle left">
      첫째, 대규모 프로젝트에 참여함으로써 고급 기술을 습득하고 경험을 쌓을 수 있다.
      <br>
      둘째, 다양한 배경을 가진 개발자들과 협력하며 국제적 감각을 기를 수 있다.
      <br>
      셋째, 오픈 소스 기여 이력은 취업 시 큰 장점으로 작용한다.
      <br>
      넷째, 프로그램의 신뢰도와 품질을 높일 수 있다.
    </p>
  </div>
  <div class="slide">
    <h1 class="title">오픈 소스 관련 이슈</h1>
    <p class="subtitle">
      Github Copilot은 AI 기반 코드 자동 완성 도구로 코드 생산성을 크게 향상시켜주어 많이 사용되고 있다.
      <br>
      <video width="320" height="240" controls>
        <source src="../public/copilot_example.mp4" type="video/mp4">
        <track kind="captions" src="../public/copilot_example.vtt" srclang="ko" label="Korean">
      </video>
    </p>
  </div>
  <div class="slide">
    <p class="subtitle left">
      하지만 이 도구가 오픈 소스 코드를 학습 데이터로 사용했다는 점에서 큰 논란이 있었다.
      <br><br>
      많은 개발자들이 자신들의 코드가 동의 없이 상업적으로 이용되었다고 주장하며, 이는 오픈 소스 라이선스 위반이라고 지적했다.
      <br><br>
      이 외에도 대기업들이 오픈 소스 프로젝트에 충분히 기여하지 않고 이익만 취하는 문제와
      <br>오픈 소스 기반 상용 제품의 라이선스 위반 사례 등이 최근 대두되고 있다.
    </p>
  </div>
  <div class="slide">
    <p class="subtitle">
      <img src="../public/aws_news.png" alt="AWS NEWS" width="800px">
    </p>
  </div>
  <div class="slide">
    <h1 class="title">노-력</h1>
    <p class="subtitle left">
      개발자와 기업 모두 라이선스의 중요성을 이해하고 준수해야 한다.
      <br>
      상업적 이용에 대한 명확한 가이드라인이 필요하다.
      <br>
      오픈 소스 개발자와 기업 간 새로운 협력 모델을 제안해야 한다.
      <br>
      (예를 들어, 기업이 오픈 소스 프로젝트에 더 적극적으로 기여하고 그 대가로 상업적 이용에 대한 권한을 얻는 방식)
    </p>
  </div>
  <div class="slide">
    <h1 class="title">결론</h1>
    <p class="subtitle">
      오픈 소스는 소프트웨어 산업의 발전에 크게 기여해왔다.
      <br>
      그러나 상업적 이용을 둘러싼 논란으로 인해 오픈 소스의 지속 가능성에 대한 우려가 생기고 있다.
      <br>
      따라서 라이선스 준수와 상호 협력을 통해 오픈 소스 생태계를 보다 건강하게 유지해야 한다.
    </p>
  </div>
  <div class="slide">
    <h1 class="title">후속 질문</h1>
    <p class="subtitle left">
      1. 오픈 소스의 미래는 어떻게 될 것인가?
      <br>
      2. 오픈 소스를 사용하여 AI를 학습시키는 것은 올바른가?
      <br>
      3. 오픈 소스의 상업적 이용에 대한 논란은 어떻게 해결되어야 하는가?
    </p>
  </div>
  <div class="slide">
    <img src="../public/repo.png" alt="Github Repo" width="800px">
  </div>
</div>

<div id="progressBar" class="progress-bar"></div>