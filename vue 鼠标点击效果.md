### 页面鼠标单击后自定义效果
  > 有许多网页 鼠标单击后会有许多炫酷的效果 这里只是做一个简单的文字效果，复杂效果就是样式的改变或者使用图片
  ```
    //vue 其中的一部分
    <div @mousedown="onMouseDown"></div>
    methods: {
      onMouseDown(){
        let text = '点击我！';
        let htmlObject = document.createElement("obj"); //创建元素
        htmlObject.onselectstart = new Function('event.returnValue=false'); //防止拖动
        document.body.appendChild(htmlObject).innerHTML = text; //将obj元素添加到页面上
        htmlObject.style.cssText = "position: fixed;left:-100%;"; //给p元素设置样式
        let f = 16, // 字体大小
				x = event.clientX - f / 2, // 横坐标
				y = event.clientY - f, // 纵坐标
				c = this.randomColor(), // 随机颜色
				a = 1, // 透明度
				s = 1.2; // 放大缩小
        
        //向上移动并直至消失
        var timer = setInterval(function () { //添加定时器
          if (a <= 0) {
            document.body.removeChild(htmlObject);
            clearInterval(timer);
          } else {
            htmlObject.style.cssText = "font-size:16px;cursor: default;position: fixed;color:" +
              c + ";left:" + x + "px;top:" + y + "px;opacity:" + a + ";transform:scale(" +
              s + ");";

            y--;
            a -= 0.016;
            s += 0.002;
          }
        }, 15)
      },
      randomColor() {
        return "rgb(" + (~~(Math.random() * 255)) + "," + (~~(Math.random() * 255)) + "," + (~~(Math
        .random() * 255)) + ")";
      }
    }
  ```
