<template>
  <ChannelList></ChannelList>
</template>

<script>
import ChannelList from './components/channelList.vue'
export default {
components : {
  ChannelList
}
}
</script>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    user-select: none;
    list-style: none;
    text-decoration: none;
    outline: none;
}

body {
    background: #000;
    font-family: "Gilroy";
}

.container {
    width: 1200px;
    margin: 0 auto;
}

</style>