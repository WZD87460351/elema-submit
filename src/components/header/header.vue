<template>
  <div class="header">
    <div class="conter-wrapper">
      <div class="avatar">
        <img width="64" height="64" :src="seller.avatar" alt="">
      </div>
      <div class="content">
        <div class="title">
          <span class="brand"></span>
          <h2>{{seller.name}}</h2>
        </div>
        <p class="desc">{{seller.description}}/{{seller.deliveryTime}}分钟送达</p>
        <div class="supports-wrapper">
          <supports v-if="seller.supports" :supports="seller.supports"></supports>
        </div>
      </div>
    </div>
    
    <div class="content-wrapper"  @click="showDetail">
    	<div class="counter" v-if="seller.supports">
    		{{seller.supports.length}}个
    		<i class="iconfont icon-keyboard_arrow_right"></i>
    	</div>
    		
    </div>
    
    <div class="bulletin-wrapper"  @click="showDetail">
    	<p>
    		<span class="icon"></span>
    		{{seller.bulletin}}
    		<i class="iconfont icon-keyboard_arrow_right"></i>
    	</p>
    	
    </div>
    
    <div class="background">
    	<img :src="seller.avatar" alt="">
    </div>
    
    <transition name="fade">
			<div class="detail-wrapper" v-show="detailShow"  @click="closeDetail">
				<div class="detail">
					<div class="inner">
						<h2>{{seller.name}}</h2>
						<div class="star-wrapper">
							<star :score="seller.score" :size="24"></star>
						</div>
						
						<div class="title">
							<div class="line"></div>
							<div class="text">优惠信息</div>
							<div class="line"></div>
						</div>
						
						<div class="supports-wrapper">
          		<supports v-if="seller.supports" :supports="seller.supports" :className="big"></supports>
        		</div>
        		
        		<div class="title">
							<div class="line"></div>
							<div class="text">商家公告</div>
							<div class="line"></div>
						</div>
						
						<p class="introduction">{{seller.bulletin}}</p>
					</div>
					
					
					
					
					<div class="close">
						<i class="iconfont icon-close"></i>
					</div>
				</div>
			</div>
    	
    </transition>
  </div>
</template>

<script>
	import supports from "../supports/supports.vue"
	import star from "../star/star.vue"
	export default {
  	props:{
			seller:{
				return:Object
			}
		},
		data(){
			return{
				detailShow:false,
				big: "big"
			}
		},
		methods:{
			showDetail(){
				this.detailShow = true;
			},
			closeDetail(){
				this.detailShow = false;
			}
		},
		components:{
			supports:supports,
			star:star
		}
	}
		
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
	@import "../../common/mixin.scss";
	.header{
		position: relative;
    height: 143px;
    background: rgba(7,17,27,.5);
    .conter-wrapper{
      padding: 24px 0px 18px 24px;
      font-size: 0;
      .avatar{
        display: inline-block;
        margin-right: 18px;
        border-radius: 2px;
        overflow: hidden;
      }
      .content{
        display: inline-block;
        vertical-align: top;
        .brand{
          vertical-align: top;
          margin-right: 6px;
          display: inline-block;
          width: 30px;
          height: 18px;
          @include bgImage(brand);
          background-size: cover;
        }
        h2{
          display: inline-block;
          line-height: 18px;
          font-size: 16px;
          font-weight: bold;
          color: #fff;
        }
        .desc{
          margin: 8px 0 10px 0;
          line-height: 12px;
          font-weight: 200;
          font-size: 12px;
          color: #fff;
        }
        .supports-wrapper{
					height: 12px;
					overflow: hidden;
        }
      }
    }
		
		.content-wrapper{
			position: absolute;
			right: 10px;
			bottom: 34px;
			.counter{
				height: 24px;
				padding: 7px 8px;
				box-sizing: border-box;
				border-radius: 12px;
				line-height: 10px;
				font-weight: 200;
				font-size: 10px;
				color: #fff;
				background-color: rgba(0,0,0,.2);
				i{
					margin-left: 0;
					font-size: 10px;
					line-height: 10px;
				}
			}
		}
		
		.bulletin-wrapper{
			box-sizing: border-box;
			padding: 0 24px 0 12px;
			position: absolute;
			left: 0;
			bottom: 0;
			width: 100%;
			height: 28px;
			line-height: 28px;
			background-color: rgba(7,17,17,.2);
			.icon{
				display: inline-block;
				vertical-align: top;
				margin-top: 7px;
				width: 24px;
				height: 13px;
				@include bgImage(bulletin);
				background-size: cover;
			}
			p{
				font-size: 10px;
				color: #fff;
				white-space: nowrap;
				overflow: hidden;
				text-overflow: ellipsis;
				i{
					position: absolute;
					right: 10px;
					top: 6px;
					font-size: 16px;
				}
			}
		}
		
		.background{
			position: absolute;
			left: 0;
			top: 0;
			width: 100%;
			height: 143px;
			z-index: -1;
			overflow: hidden;
			img{
				width: 100%;
				filter: blur(10px);
			}
		}
		
		.detail-wrapper{
			z-index: 10;
			position: fixed;
			top: 0;
			left: 0;
			width: 100%;
			height: 100%;
			background: rgba(7,17,27,.7);
			overflow: auto;
			.detail{
				position: relative;
				min-height: 100%;
				color: #fff;
/*				filter: blur(10px);*/
				backdrop-filter: blur(10px);//仅仅模糊背景，但不模糊文字
				padding-bottom: 60px;
				box-sizing: border-box;
				.inner{
					padding: 0 30px;
					color: #fff;
					h2{
						padding-top: 64px;
						line-height: 16px;
						font-size: 16px;
						font-weight: 700;
						text-align: center;
					}
					.star-wrapper{
						margin: 16px auto 28px auto;
					}
					.title{
						display: flex;
						.line{
							position: relative;
							top: -7px;
							flex: 1;
							border-bottom: 1px solid rgba(255,255,255,.2);
						}
						.text{
							font-size: 14px;
							line-height: 14px;
							font-weight: 700;
							padding: 0 12px;
						}
					}
					
					.introduction{
						font-size: 12px;
						line-height: 30px;
						padding: 20px 12px 0;
					}
				}
				.close{
					position: absolute;
					bottom: 0;
					left: 0;
					width: 100%;
					height: 60px;
					line-height: 60px;
					text-align: center;
				}
			}
			
		}
		
		.fade-enter-active, .fade-leave-active {
  		transition: opacity .5s
		}
		.fade-enter, .fade-leave-to /* .fade-leave-active in below version 2.1.8 */ {
  		opacity: 0
		}
  }
	
</style>
