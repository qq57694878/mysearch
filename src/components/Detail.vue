<template>
  <div class="root">
    <div></div>
    <div class="panel panel-primary">
      <div class="panel-heading">
        <h3 class="panel-title row"><div class="col-lg-8">{{article.title}}</div> <div class="col-lg-4">id:{{article.id}} - type:{{article.type}} - createtime:{{article.createtime}}</div></h3>
      </div>
      <div class="panel-body">
        <p v-html="article.content"></p>
      </div>
    </div>
  </div>
</template>
<script>
  export default {
    created:function(){
      this.init();
    },
    methods: {
      init(){
        var requestBody=this.id;
        console.log(requestBody);
        this.$http.post('article/findOne.json', requestBody).then((response) => {
          if (response.status == 200) {
            var responseJson = response.body;
            if (responseJson.errcode == 200) {
              this.article = responseJson.data;
              return;
            }
          }

        }, (response) => {
          console.log(response);
        });
      }

    },
    data() {
      return {
        id:this.$route.params.id,
        article: {
          title:"",
          content:"",
          type:"",
          id:"",
          createtime:""
        }
      };
    }
  }
</script>

<style scoped>
.align-right{
  text-align: right;
}
  .root {
    width: 100%;
    padding: 30px 30px;
    text-align: left;
  }

</style>
