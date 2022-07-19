<template>
  <div class="channel">
                        <a :href="`https://allplay.uz/c/${channel.id}/${channel.name}`">
                          <img class="channel-img" :src="channel.icon.url_500x500">
                          <p class="channel-title"> {{ channel.name }} </p>
                        </a>
                    </div>
</template>

<script>
export default {
props : ["channel"]
}
</script>

<style>

</style>