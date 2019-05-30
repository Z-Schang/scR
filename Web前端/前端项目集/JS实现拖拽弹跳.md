基础认知：多物体多值链式运动框架

~~~javascript
var target = {
    width : 400,
    height : 400,
    opacity : 50,
    left : 300,
    top :200
};
function startMove(obj, json, callback){
    var timer, iSpeed, iCur;
    clearInterval(obj.timer);
    obj.timer = setInterval(function(){
        var stop;
        for(var attr in json){
            if(attr == 'opacity'){
                iCur = parseFloat(getStyle(obj, attr)) * 100;
            }else{
                iCur = parseInt(getStyle(obj, attr));
            }
            iSpeed = (json[attr] - iCur) / 7;
            iSpeed = iSpeed > 0 ? Math.ceil(iSpeed) : Math.floor(iSpeed);
            if(attr == 'opacity'){
                obj.style[attr] = (iCur + iSpeed) / 100;
            }else{
                obj.style[attr] = iCur + iSpeed + 'px';
            }
            if(iCur != json[attr]){
                stop = false;
            }else{
                stop = true;
            }
        }
        if(stop){
            clearInterval(obj.timer);
            (typeof callback == 'function') ? callback() : ' ';
        }
    },30)
}
~~~

****

拖拽弹跳：

~~~javascript
	var timer;
	var lastX = oDivArray.offsetLeft;
	var lastY = oDivArray.offsetTop;
	oDivArray.onmousedown = function(e){
        clearInterval(this.timer);
		var event = e || window.event;
		var disX = e.clientX - this.offsetLeft;
		var disY = e.clientY - this.offsetTop;
		var that = this;
		var iSpeedX = 0;
		var iSpeedY = 0;
		document.onmousemove = function(e){	
			var newLeft = e.clientX - disX;
			var newTop = e.clientY - disY;
			iSpeedX = newLeft - lastX;
			iSpeedY = newTop - lastY;
			lastX = newLeft;
			lastY = newTop;
			that.style.left = newLeft + 'px';
			that.style.top = newTop + 'px';
		}
		document.onmouseup = function(){
			document.onmousemove = null;
			document.onmouseup = null;
			startMove(that, iSpeedX, iSpeedY);
		}
	}

function startMove(obj, iSpeedX, iSpeedY){
    clearInterval(obj.timer);
    //var g = 6;
    obj.timer = setInterval(function(){
        //iSpeedY += g;
        var newLeft = obj.offsetLeft + iSpeedX;
        var newTop = obj.offsetTop + iSpeedY;
        if(newTop >= document.documentElement.clientHeight - obj.offsetHeight){
            iSpeedY *= -1;
            //iSpeedX *= 0.8;
            //iSpeedY *= 0.8;
            newTop = document.documentElement.clientHeight - obj.offsetHeight;
        }
        if(newTop <= 0){
            iSpeedY *= -1;
            //iSpeedX *= 0.8;
            //iSpeedY *= 0.8;
            newTop = 0;
        }
        if(newLeft >= document.documentElement.clientWidth - obj.offsetWidth){
            iSpeedX *= -1;
            //iSpeedX *= 0.8;
            //iSpeedY *= 0.8;
            newLeft = document.documentElement.clientWidht - obj.offsetWidth;
        }
        if(newLeft <= 0){
            iSpeedX *= -1;
            //iSpeedX *= 0.8;
            //iSpeedY *= 0.8;
            newLeft = 0;
        }
        // if(Math.abs(iSpeedX) < 1){
        // 	iSpeedX = 0;
        // }
        // if(Math.abs(iSpeedY) < 1){
        // 	iSpeedY = 0;
        // }
        //if(iSpeedX == 0 && iSpeedY == 0 && newTop == //document.documentElement.clientHeight - obj.clientHeight){
        //  clearInterval(obj.timer);
        //}
        obj.style.left = newLeft + 'px';
    	obj.style.top = newTop + 'px';
    },30)
}
~~~

