<template>
  <v-app dark>
    <v-content>
      <div>
        <nuxt />
      </div>
    </v-content>

    <v-footer
      :fixed="fixed"
      app
    >
      <span>&copy; 2018 </span>
    </v-footer>

  </v-app>
</template>

<script>
export default {
  data () {
    return {
      drawer: true,
      items: [
        { icon: 'apps', title: '今日天气', to: '/' },
        { icon: 'bubble_chart', title: '未来筹募', to: '/inspire' }
      ],
      title: '欢迎来到小狐天气'
    }
  }
}
</script>

<style>
.theme--dark.v-toolbar{
  background-color: none;
}
.theme--dark.application{
  background: none;
  color: rgb(255, 255, 255);
}
.v-toolbar__content, .v-toolbar__extension {
  background-color: rgba(243, 243, 243, 0.3);
}
</style>
