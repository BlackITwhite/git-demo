## 路径标签 path
+ 属性：
    d 属性
+ 命令：
    + M 起始坐标点
    + L 后续坐标点
    + Z 首尾闭合
    + H 水平绘制(只有一个值)
    + V 垂直绘制(只有一个值)

    + A 命令绘制弧形

    + C 贝塞尔曲线
    + S 贝塞尔曲线
    + Q 贝塞尔曲线
    + T 贝塞尔曲线
    - （命令区分大小写  小写为相对坐标 大写为绝对坐标）
## A 命令
 1. X半径
 2. Y半径
 3. 角度
 4. 弧长
    - \- 0小弧 1 大弧
 5. 方向
    - \- 0逆时针 1  顺时针
 6. 终点X坐标
 7. 终点y坐标
+ 其他属性
    - stroke 颜色


<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        body {
            background-color: black;
        }

        #div1 {
            width: 400px;
            height: 400px;
            background-color: white;
        }
    </style>
    <script>

        window.onload = function () {
            var svgNS = "http://www.w3.org/2000/svg"
            var oParent = document.getElementById("div1");
            var oSvg = createTag('svg', { 'xmlns': svgNS, "width": "100%", "height": "100%" })
            function createTag(tag, objAttr) {
                var oTag = document.createElementNS(svgNS, tag);
                for (var attr in objAttr) {
                    oTag.setAttribute(attr, objAttr[attr]);
                }
                return oTag;
            }
            var arrNum = [23.61,17.10,16.05,15.40,11.72,14.94];
            var angle = 360;
            var sunNum = 0
            var outerR = 120;
            var innerR = 70;
            var centerX = 200;
            var centerY = 200;
            var outerXY = [{ "x": 320, "y": 200 }];
            var innerXY = [{ "x": 270, "y": 200 }];
            var arrColor = ["#ccccd6", "#e9d7df", "#cc5595", "#b598a1", "#7a7374", "#eea2a4", "#064", "#646"]

            for (var i = 0; i < arrNum.length; i++) {
                var agNum = arrNum[i] / 100 * angle;
                sunNum += agNum
                if(i == arrNum.length - 1){
                    sunNum = 360
                }
                var outerXx = Math.cos(sunNum * Math.PI / 180) * outerR + centerX;
                var outerYy = Math.sin(sunNum * Math.PI / 180) * outerR + centerY;
                outerXY.push({ "x": outerXx, "y": outerYy })


                var innerx = Math.cos(sunNum * Math.PI / 180) * innerR + centerX
                var intery = Math.sin(sunNum * Math.PI / 180) * innerR + centerY
                innerXY.push({ "x": innerx, "y": intery })
            }
            for (let i = 0; i < outerXY.length - 1; i++) {
                var outPath = createTag("path", {
                    "fill": arrColor[i], "d": `
                    M${outerXY[i].x} ${outerXY[i].y}
                    A${outerR} ${outerR} 0 0 1 ${outerXY[i + 1].x} ${outerXY[i + 1].y}
                    L${innerXY[i + 1].x} ${innerXY[i + 1].y}
                    A${innerR} ${innerR} 0 0 0 ${innerXY[i].x} ${innerXY[i].y}
                    Z`
                })

                oSvg.appendChild(outPath)

            }

            oParent.appendChild(oSvg);

        }

    </script>
</head>

<body>
    <div id="div1">
    </div>
</body>

</html>