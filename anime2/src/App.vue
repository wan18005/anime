<template>
  <header>
    <router-link to="/">
      <h1>The<strong>Movie</strong>Database</h1>
    </router-link>
  </header>
  <main>

   <router-view />
  </main>
<footer>
github:
</footer>


</template>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Fira Sans', sans-serif;
  &::selection 
  {
    background: transparentize(#42B883, 0.5);
  }
}
body {
  background-color: #35495E;
}
a {
  text-decoration: none;
}
header {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 10px 16px;
  background-color: #080101d5;
  box-shadow: 0px 0px 6px rgba(0, 0, 0, 0.1);
  h1 {
    color: #FFF;
    font-size: 28px;
    span {
      color: #42B883;
    }
    strong {
			color: rgba(4, 113, 255, 0.877);
		}
  }
}
footer
{ 
  color:#FFF;
  padding: 20px 2px;
}
</style>
