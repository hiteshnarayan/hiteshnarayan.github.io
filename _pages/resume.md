---
layout: page
title: Resume
permalink: /resume/
nav: true
---


<style>
  body, html {
      margin: 0;
      padding: 0;
      height: 100%;
      overflow: hidden;
  }
  iframe {
      width: 100%;
      height: 100%;
      border: none;
  }
  .fullscreen-button {
      position: absolute;
      top: 10px;
      right: 10px;
      z-index: 1000;
      padding: 10px 20px;
      background-color: #007bff;
      color: white;
      border: none;
      cursor: pointer;
  }
</style>

<button class="fullscreen-button" onclick="toggleFullScreen()">Full Screen</button>

<div class="content">
  <iframe id="pdfFrame" src="../assets/pdf/Hitesh%20Narayana.pdf" allowfullscreen></iframe>
</div>

<script>
  function toggleFullScreen() {
      var iframe = document.getElementById('pdfFrame');
      if (iframe.requestFullscreen) {
          iframe.requestFullscreen();
      } else if (iframe.mozRequestFullScreen) { 
          iframe.mozRequestFullScreen();
      } else if (iframe.webkitRequestFullscreen) { 
          iframe.webkitRequestFullscreen();
      } else if (iframe.msRequestFullscreen) { 
          iframe.msRequestFullscreen();
      }
  }
</script>