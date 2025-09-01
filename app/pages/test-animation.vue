<template>
    <div class="orbit-container">
      <div class="orbiting-element">
        ⭐
      </div>
    </div>
  </template>
  
  <style scoped>
  .orbit-container {
    width: 200px;
    height: 200px;
    position: relative;
    border: 1px dashed gray;
    border-radius: 50%;
    margin: 2rem auto;
  
    animation: orbit 5s linear infinite;
  }
  
  .orbiting-element {
    width: 50px;
    height: 50px;
    position: absolute;
    top: 0;
    left: 50%;
    transform: translateX(-50%);
    font-size: 2rem;
    text-align: center;
    line-height: 50px;
  
    animation: counter-rotate 5s linear infinite;
  }
  
  @keyframes orbit {
    from { transform: rotate(0deg); }
    to { transform: rotate(360deg); }
  }
  
  @keyframes counter-rotate {
    from { transform: rotate(0deg); }
    to { transform: rotate(-360deg); }
  }
  </style>
  