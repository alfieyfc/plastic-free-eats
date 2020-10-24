<template>
  <div id="bar">
    <button id="menu-btn" type="button"><img id="menu-img" alt="Menu" src="https://imgur.com/1A4zm0A.png"></button>
    <input id="search" type="text" placeholder="Search for locations"/>
    <button id="search-btn"><img id="menu-img" alt="Menu" src="https://i.imgur.com/RUHKWNZ.png"></button>
    
  </div>
</template>

<script>
  export default {
    data: function () {
      return {
        items: (function () {
          var it = [];
          for (var i = 0; i < 100; i++) it.push(i+1);
          return it;
        })()
      }
    },
    methods: {
    }
  }
</script>

<style scoped>
#bar {
  width: 65%;
  border-color: #FDFDFD;
}
#menu-img {
  width: 100%;
  vertical-align: middle;
}
#menu-btn, #search-btn {
  border: 0;
  background-color: transparent;
  vertical-align: middle;
  height: 45px;
  width: 45px;
  margin: 10px;
}
#search {
  vertical-align: middle;
  height: 40px;
  margin: 10px 0px 10px 10px;
  font-size: 18px;
  width: calc(100% - 148px);
}
</style>