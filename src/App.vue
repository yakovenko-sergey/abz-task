<template>
  <vMenu :scrollTo="scrollTo"/>
  <div class="app__content">
    <vHeader :scrollTo="scrollTo"/>
    <vUsers :scrollTo="scrollTo" :requestToApi="requestToApi"  ref="users"/>
    <vSignUp :requestToApi="requestToApi" @renewUsers="renewUsers"/>
  </div>
  <vFooter/>
  <router-view/>
</template>

<script>
  import vMenu from "../src/components/Menu"
  import vHeader from "../src/components/Header"
  import vUsers from "../src/components/Users"
  import vSignUp from "../src/components/Signup"
  import vFooter from "../src/components/Footer"
  export default {
    name: "App",
    components:{
      vMenu,
      vHeader,
      vUsers,
      vSignUp,
      vFooter
    },
    data (){
      return {
        users:[],
      }
    },
    methods:{
      renewUsers(){
        this.$refs.users.usersArr=[];
        this.$refs.users.getUsers('https://frontend-test-assignment-api.abz.agency/api/v1/users?page=1&count=6');
      },
      async requestToApi (url,config={}){
        try{
          const response = await fetch(url,config);
          const data = await response.json();
          return data;
        }
        catch (e) {
          console.log('error',e);
        }
      },
      scrollTo(goto){
          document.querySelector(goto).scrollIntoView({
          behavior: "smooth",
          block: "start"
        })
      }
    }
  }
</script>

<style>
  html, body, div, span, applet, object, iframe,
  h1, h2, h3, h4, h5, h6, p, blockquote, pre,
  a, abbr, acronym, address, big, cite, code,
  del, dfn, em, img, ins, kbd, q, s, samp,
  small, strike, strong, sub, sup, tt, var,
  b, u, i, center,
  dl, dt, dd, ol, ul, li,
  fieldset, form, label, legend,
  table, caption, tbody, tfoot, thead, tr, th, td,
  article, aside, canvas, details, embed,
  figure, figcaption, footer, header, hgroup,
  menu, nav, output, ruby, section, summary,
  time, mark, audio, video,button {
    margin: 0;
    padding: 0;
    border: 0;
    font-size: 100%;
    font: inherit;
    vertical-align: baseline;
  }

  img{
    width:100%;
  }
  /* HTML5 display-role reset for older browsers */
  article, aside, details, figcaption, figure,
  footer, header, hgroup, menu, nav, section {
    display: block;
  }
  body{
    background: #F8F8F8;
  }
  .app__content{
    max-width: 1170px;
    margin: auto;
  }
</style>
