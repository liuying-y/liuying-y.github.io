---
layout: full-page
title: 视差滚动 02-transform
date: 2024-12-29 01:49
category: [code, front-end]
author: 
tags: []
summary: 
---
<style>
  .home-root {
    perspective: 1px;
    height: 100vh;
    overflow-x: hidden;
    overflow-y: auto;
    position: relative;
  }

  .layer {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-size: cover;
    background-position: center;
    transform: translateZ(var(--z));
    backface-visibility: hidden; /* 改善性能 */
  }

  #title-1 {
    z-index: 2;
    top: 30vh;
  }

  #ani-1-1 {
    position: relative;
    margin-top: 10vh;
    margin-left: 5vw;
    transform: translateZ(-0.02px);
    top: 50vh;
  }

  #ani-1-2 {
    position: relative;
    margin-top: 10vh;
    top: 120vh;
    transform: translateZ(-0.9px);
  }
  #ani-2-1 {
    margin-top: 10vh;
    top: 200vh;
  }

  #ani-2-2 {
    margin-top: 8vh;
    margin-left: 5vw;
    top: 220vh;
  }

  #ani-2-2 li {
    margin-top: 4vh;
  }

  .contact-alias {
    text-transform: uppercase;
  }

  #ani-3-1 {
    margin-top: 5vh;
    text-align: center;
    text-transform: uppercase;
    top: 330vh;
  }

  #ani-3-2 {
    list-style: none;
    display: flex;
    margin: 20vh auto 0;
    width: fit-content;
    top: 330vh;
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
  <h1 id="title-1" class="layer" data-z="-1">{{ page.title }}</h1>
  <h2 id="ani-1-1" class="layer" data-z="-1">基于transform</h2>
  <h3 id="ani-1-2" class="layer" data-z="-0.2">总体评价：用css实现，快速上手，但是要做出好效果非常不容易</h3>
  <h2 id="ani-2-1" class="layer" data-z="-1">技术核心有几点</h2>
  <ul id="ani-2-2" class="layer" data-z="-0.1">
    <li>父元素设置 perspective</li>
    <li>子元素设置 translateZ</li>
    <li>滚动时更新 translateY</li>
  </ul>
  <ui id="ani-3-2" class="layer" data-z="-1">
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
  <h6 id="ani-3-1" class="layer" data-z="-1">Contact</h6>
</div>

<script>
const scene = document.querySelector('.home-root');
const layers = document.querySelectorAll('.layer');

function handleScroll() {
  const scrollPosition = scene.getBoundingClientRect().top;
  layers.forEach(layer => {
    const depth = parseFloat(layer.dataset['z']);
    const factor = -(depth / Math.abs(depth)) * Math.min(Math.abs(depth), Math.abs(scrollPosition));
    layer.style.transform = `translateZ(${depth}px) translateY(${factor}px)`;
  });
}

// 监听滚动事件
scene.addEventListener('scroll', handleScroll);
window.addEventListener('resize', handleScroll);

// 初始化调用
handleScroll();

</script>