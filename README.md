# DigitTwins
没什么好说的，超简单的一个数字连连看

##代码
####游戏规则：翻开两张牌，一样的话就一直显示，不一样的话就翻回背面，直到所有牌翻开后获胜
````javascript
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>数字连连看</title>
  <link rel="stylesheet" href="css/style.css">
	<script src="js/jquery-1.9.1.min.js"></script>
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
	<script type="text/javascript">
	$(function(){	
     var a=5;var b=4;
     var arrA = []; 
     for(var i=1;i<a*b/2+1;i++){
      arrA.push(i);
      arrA.push(i);
     }
     arrA.sort( function(a, b) {
        return Math.random()>.5 ? -1 : 1;
     });
     $(".content").width(67*b);
     $(".content").height(67*a);
     for(var i=1;i<a*b+1;i++){
       $(".content").append('<div class="cell" id="'+i+'"><div class="cell-bg"></div><div class="cell-num">'+arrA[i-1]+'</div></div>');
     }

     var open=0,open1=0,open2=0,win=0;
     $(".cell").click(function(){
        if(!$(this).hasClass("tran")&&open!=2){
          open++;
          $(this).addClass("tran");
          var id=$(this).attr("id");
          if(open==1){open1=id;}
          if(open==2){open2=id;}
          setTimeout(function(){
            $("#"+id).find(".cell-num").addClass("zindex");
          },200);
          if (open==2) {         
            if($("#"+open1).find(".cell-num").text()!=$("#"+open2).find(".cell-num").text()){
              setTimeout(function(){
                $("#"+open1).removeClass("tran");
                $("#"+open2).removeClass("tran");
                setTimeout(function(){
                   $("#"+open1).find(".cell-num").removeClass("zindex");
                   $("#"+open2).find(".cell-num").removeClass("zindex");
                   open=0;
                },200);
              },800);
            }else{
               open=0;
               win++;
               if(win==a*b/2){
                setTimeout(function(){alert("YOU WIN !!!!!!!!");},500);
               }
            }
          };
        }
     })
  })
	</script>
</head>
<body>
<div class="content">
  
</div>


</body>
</html>
```
