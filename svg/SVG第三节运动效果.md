# js 原生运动
+ JQ的animate
+ duration 运动时间
+ easing 运动形式 swing  linear
+ step  监听运动状态的比值关系 （a,b）
    + b.pos // 0-1
## 添加运动效果
+ 一般写法 > ${"div1"}.animate({},1000,"linear",function(){});
+ 两个json写法
    ~~~javascript 
     ${"div1"}.animate({
         move:"auto",
     },{
         duration:1000,
         easing:"swing",
         step:function(a,b){
             // b.pos
         }
     })
    ~~~
# svg 运动标签
+ animate svg运动标签

+ attrbuteName 指定要运动的属性
+ dur  指定运动时间
+ from => to 从多少运动到多少