	
	var CanvasDrawr = function(options){
		//设定画布信息
		var canvas = document.getElementById(options.id),
			ctxt=canvas.getContext('2d');
	    var createImgBtn = document.getElementById(options.createImgBtn);
	    var storageImgDiv = document.getElementById(options.storageImgDiv);
	    var clearCanvasBtn = document.getElementById(options.clearBtn);
	
		canvas.style.width='100%';
		canvas.width=canvas.offsetWidth;
		canvas.style.width='';
		//设定来自options的属性
		ctxt.lineWidth=options.size || Math.ceil(Math.random*35);
		ctxt.lineCap=options.lineCap || 'round';
		ctxt.pX=undefined;
		ctxt.pY=undefined;
		var lines=[,,];
		var offset = $(canvas).offset();
	
		var self={
			//初始化，绑定touchstart 和 touchmove事件
			init:function(){
				canvas.addEventListener('touchstart',self.preDraw,false);
				canvas.addEventListener('touchmove',self.draw,false);
	            createImgBtn.onclick=function(){
	                var url=canvas.toDataURL('image/png'),
	                img=new Image();
	                img.src=url;
	                storageImgDiv.innerHTML="";
	                storageImgDiv.appendChild(img);
	            };
	            clearCanvasBtn.onclick=function(){
	                ctxt.clearRect(0,0,canvas.width,canvas.height);  
	            }
			},
			preDraw:function(event){
				//当touchstart时，获取相对canvas的x\y位置，画笔的颜色
				$.each(event.touches,function(i,touch){
					var id=touch.identifier,
						// colors  = ["red", "green", "yellow", "blue", "magenta", "orangered"],
						mycolor = "black";
						lines[id]={
							x:this.pageX - offset.left,
							y:this.pageY - offset.top,
							color:mycolor,
						}
				});
				event.preventDefault();
			},
			draw:function(event){
				//touchmove开始划线
				var e = event,
					hmm = {};
				$.each(event.touches,function(i,touch){
					var id=touch.identifier,
						moveX=this.pageX-offset.left-lines[id].x,
						moveY=this.pageY-offset.top-lines[id].y;//移动的x\y
	
					var ret=self.move(id,moveX,moveY);//canvas的画线
					lines[id].x=ret.x;
					lines[id].y=ret.y;
				})
				event.preventDefault();
			},
			move:function(i,changeX,changeY){
				ctxt.strokeStyle=lines[i].color;
				ctxt.beginPath();
				ctxt.moveTo(lines[i].x,lines[i].y);
				ctxt.lineTo(lines[i].x + changeX, lines[i].y + changeY);
				ctxt.stroke();
				ctxt.closePath();
				return {
					x:lines[i].x+changeX,
					y:lines[i].y+changeY
				};
			},
		}
		
		return self.init();//运行init	
	}
	$(function(){
		var drawing_canvas = new CanvasDrawr({
	        id: "sign_div", 
	        size:1,
	        createImgBtn: "create_btn",
	        storageImgDiv: "img_div",
	        clearBtn:"clear_btn",
	    });
	})