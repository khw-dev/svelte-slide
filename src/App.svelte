<script lang="ts">
  import { onMount } from 'svelte';

  let currentIndex: number = 0;
  let totalSlides: number = 4;

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
    --slide-width: 4;
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
  }

  .slide h1, .slide p {
    margin: 0;
  }

  .title {
    font-size: 4.5rem;
  }

  .subtitle {
    font-size: 1.5rem;
    text-align: left;
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
      <p class="subtitle">오픈 소스 기여와 상업적 이용</p>
  </div>
  <div class="slide">
    <h1 class="title">오픈 소스란?</h1>
    <p class="subtitle">
      오픈 소스 소프트웨어는 개방형 협업을 통해 개발되고 유지 관리되는 소프트웨어이다.
      <br>일반적으로 무료로 누구나 원하는 대로 사용, 검사, 변경 및 재배포 할 수 있다.
      <a href="https://www.ibm.com/kr-ko/topics/open-source" target="_blank" class="source">[1]</a>
    </p>
  </div>
  <div class="slide">
    <h1 class="title">오픈 소스의 기본 원칙</h1>
    <p class="subtitle">
      첫째, 커뮤니티 중심의 협력. 전 세계 개발자들이 자발적으로 참여하여 코드를 개선하고 버그를 수정한다.
      <br>
      둘째, 투명성과 공개 개발. 모든 개발 과정이 공개되어 누구나 검토하고 의견을 제시할 수 있다.
      <br>
      셋째, 자유로운 사용, 수정, 배포. 이는 오픈 소스 소프트웨어의 가장 큰 특징으로, 사용자에게 광범위한 자유를 제공한다.
    </p>
  </div>
  <div class="slide">
    <h1 class="title">오픈 소스의 기본 원칙</h1>
    <p class="subtitle">
      첫째, 대규모 프로젝트에 참여함으로써 고급 기술을 습득하고 경험을 쌓을 수 있다.
      <br>
      둘째, 다양한 배경을 가진 개발자들과 협력하며 국제적 감각을 기를 수 있다.
      <br>
      셋째, 오픈 소스 기여 이력은 취업 시 큰 장점으로 작용한다.
    </p>
  </div>
</div>

<div id="progressBar" class="progress-bar"></div>