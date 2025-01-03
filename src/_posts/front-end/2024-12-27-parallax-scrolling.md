---
layout: full-page
title: 视差滚动 01-gsap
date: 2024-12-27 22:43
category: [code, front-end]
author: 
tags: []
summary: 
---
<style>
  .home-root {
    position: relative;
    height: calc(100vh * 2.5);
    touch-action: none;
  }
  .home-background::before {
    content: ' ';
    position: fixed;
    top: 0;
    bottom: 0;
    left: 6vw;
    width: 3px;
    background-color: var(--ly-font-color-2);
  }
  .home-slice {
    width: 100vw;
    height: 50vh;
    position: relative;
    box-sizing: border-box;
    padding-left: 4vw;
    padding-right: 4vw;
    padding-top: 20vh;
  }

  .home-slice h2 {
    margin-left: 5vw;
  }

  .home-slice h3 {
    margin-left: 10vw;
  }

  #title-1 {
    z-index: 2;
    margin-top: 20vh;
    position: fixed;
  }

  #section-1 {
    padding-top: 20vh;
  }

  #section-3 {
    height: 100vh;
  }


  #ani-1-1 {
    position: relative;
    margin-top: 25vh;
    margin-left: 5vw;
  }

  #ani-1-2 {
    position: relative;
    margin-top: 10vh;
  }
  #ani-2-1 {
    margin-top: 10vh;
  }

  #ani-2-2 {
    margin-top: 8vh;
    margin-left: 5vw;
  }

  #ani-2-2 li {
    margin-top: 4vh;
  }

  #section-3 {
  }

  .contact-alias {
    text-transform: uppercase;
  }

  #ani-3-1 {
    margin-top: 5vh;
    text-align: center;
    text-transform: uppercase;
  }

  #ani-3-2 {
    list-style: none;
    display: flex;
    margin: 20vh auto 0;
    width: fit-content;
  }

  #ani-3-2 li {
    margin-right: 1.1rem;
    margin-left: 1.1rem;
  }

  .icon {
    position: relative;
    font-size: 2.2rem;
    line-height: 1;
  }

  .icon::before {
    font-family: 'remixicon' !important;
    font-size: 2.2rem;
    position: relative;
    transition: all .2s ease;
    display: inline-block;
  }

  .icon-tip {
    pointer-events: none;
    touch-action: none;

    font-size: 0.5rem;
    color: var(--ly-background-color);
    background-color: var(--ly-font-color-2);
    padding: 5px;
    border-radius: 5px;

    opacity: 0;
    position: absolute;
    bottom: 100%;
    left: 50%;
    transform: translateX(-50%) translateY(-2.2rem);
    transition: all .2s ease;
  }

  @keyframes shake {
    0% { transform: translate(1px, 1px) rotate(0deg); }
    10% { transform: translate(-1px, -2px) rotate(-1deg); }
    20% { transform: translate(-3px, 0px) rotate(1deg); }
    30% { transform: translate(3px, 2px) rotate(0deg); }
    40% { transform: translate(1px, -1px) rotate(1deg); }
    50% { transform: translate(-1px, 2px) rotate(-1deg); }
    60% { transform: translate(-3px, 1px) rotate(0deg); }
    70% { transform: translate(3px, 1px) rotate(-1deg); }
    80% { transform: translate(-1px, -1px) rotate(1deg); }
    90% { transform: translate(1px, 2px) rotate(0deg); }
    100% { transform: translate(1px, -2px) rotate(-1deg); }
  }
  .icon:hover::before {
    animation: shake 0.82s cubic-bezier(.36,.07,.19,.97) both;
    transform: translate3d(0, 0, 0);
    backface-visibility: hidden;
    perspective: 1000px;
  }
  .icon:hover .icon-tip {
    transform: translateX(-50%) translateY(-1rem) scale(1.5);
    opacity: 1;
  }

</style>
<div class="home-root">
  <section class="home-background"></section>
  <!-- <section id="section-0"><br /></section> -->
  <h1 id="title-1" class="full-background">{{ page.title }}</h1>
  <section id="section-cover" class="home-slice">
    <h2 id="ani-1-1" class="">基于gsap</h2>
    <h3 id="ani-1-2" class="">总体评价：可以专注于效果，但是调整效果太消耗精力啦</h3>
  </section>
  <section id="section-2" class="home-slice">
    <h2 id="ani-2-1" class="full-background">还有一些问题，比如</h2>
    <ul id="ani-2-2">
      <li>有几个参数一直没有读懂</li>
      <li>滚动时希望让界面停顿，我一直没解</li>
      <li>还有页面刷新时滚动位置被保存了！！</li>
      <li>另外，修改的时候要小心一点</li>
    </ul>
  </section>
  <section id="section-3" class="home-slice">
    <ui id="ani-3-2">
      {%- for s in site.social -%}
        <li>
          <a title="{{ s.alias }}" class="contact-alias" href="{{ s.url }}" target="_blank">
            <i class="{{ s.icon }} icon">
              <h5 class="icon-tip">{{ s.alias }}</h5>
            </i>
          </a>
        </li>
      {%- endfor -%}
    </ui>
    <h6 id="ani-3-1" class="">Contact</h6>
  </section>
</div>
<script src="/assert/libs/gsap.min.js"></script>
<script src="/assert/libs/ScrollTrigger.min.js"></script>
<script>
  // section 1
  var list = [{
    triggerInfo: {
      trigger: "#section-cover",
      scrub: 0.5,
      pin: true,
      start: "top top",
      end: "+=100%",
    },
    anamations: [{
      target: '#title-1',
      method: 'from',
      params: { y: '50vh' },
    }, {
      target: '#ani-1-1',
      method: 'from',
      params: { autoAlpha: 0 },
      position: '+=100%',
    }, {
      target: '#ani-1-1',
      method: 'from',
      params: { y: '30vh' },
      position: '-=50%',
    }, {
      target: '#ani-1-2',
      method: 'from',
      params: { y: '30vh', autoAlpha: 0 },
      position: '+=100%',
    }, {
      target: '#title-1',
      method: 'to',
      params: { y: '-15vh' },
      position: '+=100%',
    }, {
      target: '#ani-1-1',
      method: 'to',
      params: { y: '-30vh', autoAlpha: 0 },
      position: '-=100%',
    }, {
      target: '#ani-1-2',
      method: 'to',
      params: { y: '-30vh', autoAlpha: 0 },
      position: '-=100%',
    }],
  }, {
    triggerInfo: {
      trigger: "#section-2",
      scrub: 1,
      pin: true,
      start: "top top",
      end: "+=100%",
    },
    anamations: [{
      target: '#ani-2-2',
      method: 'from',
      params: { y: '30vh', autoAlpha: 0 },
    }, {
      target: '#ani-2-2',
      method: 'to',
      params: { y: '0' },
    }, {
      target: '#ani-2-2',
      method: 'to',
      params: { y: '30vh', autoAlpha: 0 },
    }, {
      target: '#ani-2-1',
      method: 'to',
      params: { y: '30vh', autoAlpha: 0 },
      position: '-=100%',
    }],
  }, {
    triggerInfo: {
      trigger: "#section-3",
      scrub: 0.5,
      pin: true,
      start: "top top",
      end: "+=100%",
    },
    anamations: [{
      target: '#ani-3-2',
      method: 'from',
      params: { y: '-50vh', scale: 1.2, autoAlpha: 0, transformOrigin: "center center" },
    }, {
      target: '#ani-3-1',
      method: 'from',
      params: { rotate: 100, scale: 0, autoAlpha: 0, transformOrigin: "center center" },
    }],
  }];

  function start() {
    list.forEach(function(list_ele) {
      var tl1 = gsap.timeline({
        scrollTrigger: list_ele.triggerInfo,
      });
      list_ele.anamations.forEach((ele) => {
        console.log('[mm]', ele.method);
        tl1[ele['method']](ele.target, Object.assign({ anticipatePin: 1}, ele.params), ele.position);
      });
    });
  }

  document.addEventListener("DOMContentLoaded", function() {
    gsap.registerPlugin(ScrollTrigger);
    start();
  });
</script>