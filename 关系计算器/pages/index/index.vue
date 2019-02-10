<template>
	<view class="content">
		<div id="history">
			{{history}}
		</div>
		<div id="show">
			{{show}}
		</div>
		<div id="btn">
			<div v-for="(value,callName) in call" @click="calculate(value)">{{callName}}</div>
<!-- 			<div v-for="call">夫</div>
			<div>妻</div>
			<div>返回</div>
			<div>清空</div>
			<div>父</div>
			<div>母</div>
			<div>兄</div>
			<div>弟</div>
			<div>姐</div>
			<div>妹</div>
			<div>子</div>
			<div>女</div>
			<div>互查</div>
			<div>=</div> -->
		</div>
        
	</view>
</template>

<script>
	var relationship = require("../../relationship.min.js");
	export default {
		data() {
			return {
				title: '亲属关系计算机',
				history:"",
				show:"",
				call:{
					"夫":"丈夫",
					"妻":"妻子",
					"返回":"back",
					"清空":"empty",
					"父":"父亲",
					"母":"母亲",
					"兄":"哥哥",
					"弟":"弟弟",
					"姐":"姐姐",
					"妹":"妹妹",
					"子":"儿子",
					"女":"女儿",
					"互查":"anti",
					"=":"result"
				}
			}
		},
		onLoad() {

		},
		methods: {
			calculate:function(e){
				let anti=false;
				switch (e){
					case "empty":
						this.history="";
						this.show="";
						return 0;
					case "result":
						return 0;
					case "anti":
						anti=true;
						break;
					case "back":
						let old=this.history;
						let sp=old.split("的");
						if(sp.length>1){
							console.log(sp);
							sp.splice(-1,1);
							console.log(sp);
						}
						else{
							this.history="";
							this.show="";
							return 0;
						}
						if(sp.length>1){
							sp=sp.join("的");
							console.log(sp);
							this.history=sp;
						}
						else{
							this.history=sp[0];
							this.show=sp[0];
							return 0;
						}

						break;
					default:
						this.history+=(this.history=="")?e:("的"+e);
						break;
				}
				// this.history+=(this.history=="")?e:("的"+e);
				var options = {
					text:this.history,		//输入的文本
					// sex:0,			//自己的性别：0女性,1男性
					type:'default',		//转换类型：'default'算称谓,'chain'算关系(此时reverse无效)
					reverse:anti		//称呼方式：true对方称呼我,false我称呼对方
				};
				let result=relationship(options).join("/");
				console.log(result)
				this.show=result?result:"计算器已经被你玩坏了哟!";
			}
		}
	}
</script>

<style>
/* 	uni-page-wrapper{
		background: #f5f5f5;
	} */
	.content {
		text-align: center;
		height: 400upx;
	}
    .logo{
        height: 200upx;
        width: 200upx;
        margin-top: 200upx;
    }
	.title {
		font-size: 36upx;
		color: #8f8f94;
	}
	#show,#history{
		width: 100%;
		padding-right: 3%;;
		min-height:35px;
		line-height: 35px;
		font-size: 30px;
		text-align: right;
		position: fixed;
		bottom: 370px;
		left: 0px;
		overflow: scroll;
	}
	#show{
		width: 100%;
		height:35px;
		bottom: 333px;
		left: 0px;
	}
	#btn{
		width: 100vw;
		position: fixed;
		height:320px;
		bottom: 0px;
		left: 0px;
	}
	#btn>div{
		float: left;
		width: 24.9%;
		height:80px;
		line-height: 80px;
		background: #f9f9f9;
		border: #d5d5d5 0.2px solid
	}
	#btn>div:nth-of-type(13),#btn>div:nth-of-type(14){
		width:49.5%;
		border-bottom: 0;
	}
	#btn>div:nth-of-type(1),#btn>div:nth-of-type(5),#btn>div:nth-of-type(9),#btn>div:nth-of-type(13){
		border-left:0;
	}
	#btn>div:nth-of-type(4),#btn>div:nth-of-type(8),#btn>div:nth-of-type(12),#btn>div:nth-of-type(14){
		border-right:0;
	}
</style>
