<template>
  <div id="app">
    <div class="addcart"></div>
    <img id="end" src="./assets/net.png"></img>
    <!--<img id="basketball" class="u-flyer" src="./assets/basketball.png" style="display: block;">-->
    <div id="msg">球进了！</div>
  </div>
</template>

<script>
  import fly from './../static/jquery.fly.min.js'

  export default {
    name: 'App'
  }
  $(function () {
    var offset = $("#end").offset();
    var ingFlg = false;
    $(".addcart").on('mouseup', function (event) {
      if (ingFlg) {
        return;
      }
      //隐藏篮球
      $('.addcart').css('display', 'none');
      ingFlg = true;
      var addcart = $(this);
      var flyer = $('<div class="u-flyer" />');
      //var flyer = $('#backetball');
      flyer.fly({
        speed: 1.1,//越大越快，默认1.2
        vertex_Rtop: 1, //运动轨迹最高点top值，默认20（越小弧度越大）
        start: {
          left: event.pageX - 30,
          top: event.pageY - 30
        },
        end: {
          left: offset.left,
          top: offset.top + 10,
          width: '64px',
          height: '64px'
        },
        onEnd: function () {
          //显示篮球
          $('.addcart').css('display', 'block');
          ingFlg = false;
          $("#msg").show().animate({width: '250px'}, 200).fadeOut(1000);
          //addcart.css("cursor", "default").removeClass('orange').unbind('click');
          this.destory();
        }
      });
    });

    //点击篮球事件
  });
</script>

<style>
  @import '.././static/main.css'; /*引入css文件*/

  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
