<template>
  <div>
    <link rel="preconnect" href="https://fonts.gstatic.com" />
    <link
      href="https://fonts.googleapis.com/css2?family=Fira+Code&display=swap"
      rel="stylesheet"
    />
    <Nuxt />
  </div>
</template>

<style>
html {
  font-family: 'Source Sans Pro', -apple-system, BlinkMacSystemFont, 'Segoe UI',
    Roboto, 'Helvetica Neue', Arial, sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
}

html,
body,
#__nuxt,
#__layout,
#__layout > div {
  height: 100vh;
  width: 100vw;
  background-color: #141821 !important;
  color: white;
  white-space: nowrap;
}

code {
  color: white !important;
  display: block;
  font-family: Fira Code, Consolas, Courier New, monospace;
}

.codeviewer {
  line-height: 1.5rem;
  white-space: pre-wrap;
  font-size: 0.9em;
  padding-bottom: 5rem !important;
}
</style>
