<template>
  <div class="container">
    <div class="item" v-for="image in quotes" v-bind:key="image">
      <img :src="image"/>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Main',
  data(){
    return{
      quotes:[]
    }
  },
  methods:{
    scrolldetect: function () {
      window.onscroll = () => {
        let bottomOfWindow = Math.max(window.pageYOffset, document.documentElement.scrollTop, document.body.scrollTop) + window.innerHeight >= document.documentElement.offsetHeight+10

        if (bottomOfWindow) {
          this.loadquotes()
        }
      }
    },
    loadquotes:function () {
      const the=this;
      for (let pas = 0; pas < 5; pas++) {
        fetch('https://inspirobot.me/api?generate=true')
            .then(response => response.text())
            .then((res) =>  {
              the.quotes.push(res)
            })
      }

    }
  },
  mounted:function (){
    this.loadquotes()
    this.scrolldetect()
  }

}
</script>
