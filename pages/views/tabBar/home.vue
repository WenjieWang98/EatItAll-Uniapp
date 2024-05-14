<template>
	<view class="home">
		<!-- 顶部 -->
		<headers :colors="colors" :locations="locations" :swiperList="swiperList"></headers>
		<!-- 推荐分类菜单 与tab分类中不同 -->
		<classList :categoryList="categoryList"></classList>
		<!-- 公告 -->
		<notice :colors="colors" :noticeList="noticeList"></notice>
		<!-- 栏目 -->
		<!-- <column></column> -->
		<!-- 广告图 -->
		<!-- <banner></banner> -->
		<!-- 热门标题 -->
		<hotstitle :colors="colors"></hotstitle>
		<!-- 推荐商品列表 -->
		<recommend :colors="colors" :dataList="dataList" :loading="loading" :bottoms="bottoms"></recommend>
		<!-- 右侧悬浮菜单栏 -->
		<suspension :scrollShow="scrollShow" :colors="colors"></suspension>
	</view>
</template>

<script>
	var app = getApp();
	import headers from '../../commponent/home/header';
	import classList from '../../commponent/home/classList';
	import notice from '../../commponent/home/notice';
	import column from '../../commponent/home/column';
	import banner from '../../commponent/home/banner';
	import hotstitle from '../../commponent/home/hotstitle';
	import recommend from '../../commponent/home/recommend';
	import suspension from '../../commponent/home/suspension';
	import {
		getlocation
	} from '@/utils/auth.js'
	export default {
		data() {
			return {
				colors: '',
				bottoms: '100',
				scrollShow: false, //是否显示悬浮菜单
				categoryList: [{ //分类列表
					id: 1,
					name: '食品盲盒',
					img: "/static/images/class/food-cookie.png"
				}, {
					id: 2,
					name: '商家入驻',
					img: "/static/images/log.png"
				},],
				// 商品列表
				dataList: [{
						title: 'DUNKINDONUTS唐恩都乐美国甜甜圈盲盒',
						type: 1,
						goods_id: 201,
						money: '19.90',
						number: 1,
						hmoney: '45.90',
						img: '/static/images/goods/one.jpg',
						youhui: true,
						baoyou: false,
						status: 1, //商品过期状态  0正常  1已失效
						stock: 600,
						sku: [{
							sku_id: 1,
							skuname: '口味',
							child: [{
									tagname: '醇黑巧克力【20枚】',
									id: 2011,
									imgs: 'http://img10.360buyimg.com/n1/jfs/t1/86401/35/12206/357766/5e43b59cE5a7aa4dd/0753be765166c195.jpg',
									money: '175.78'
								},
								{
									tagname: '草莓味【8枚】',
									id: 2012,
									imgs: 'http://img11.360buyimg.com/n1/jfs/t1/74434/3/6892/331750/5d512febE54e891c4/0096ad20c3c20d23.jpg',
									money: '35.90'
								}
							]
						}],
						skuArr: [{
								goods_sku_arr: ['2011'],
								goods_sku_text: '醇黑巧克力【20枚】',
								img: 'http://img10.360buyimg.com/n1/jfs/t1/86401/35/12206/357766/5e43b59cE5a7aa4dd/0753be765166c195.jpg',
								money: '175.78',
								stock: 345
							},
							{
								goods_sku_arr: ['2012'],
								goods_sku_text: '草莓味【8枚】',
								img: 'http://img11.360buyimg.com/n1/jfs/t1/74434/3/6892/331750/5d512febE54e891c4/0096ad20c3c20d23.jpg',
								money: '35.90',
								stock: 255
							},
						]
					},
					{
						title: '面包盲盒',
						type: 2,
						goods_id: 202,
						money: '29.9',
						number: 75,
						hmoney: '39.90',
						img: '/static/images/goods/two.jpg',
						youhui: false,
						baoyou: true,
						status: 0, //商品过期状态  0正常  1已失效
						stock: 100,
						sku: [{
							sku_id: 1,
							skuname: '口味',
							child: [{
									tagname: '500g甜甜圈（彩针款）',
									id: 2021,
									imgs: 'http://img14.360buyimg.com/n1/jfs/t1/72185/1/7121/222065/5d5377d5E46e681fa/6f100c77965b9165.jpg',
									money: '39.90'
								},
								{
									tagname: '500g甜甜圈（拉花款）',
									id: 2022,
									imgs: 'http://img14.360buyimg.com/n1/jfs/t1/72191/2/6973/239664/5d5377d5Ef952d7d9/606e70d2b6dd44d2.jpg',
									money: '39.90'
								}
							]
						}],
						skuArr: [{
								goods_sku_arr: ['2021'],
								goods_sku_text: '500g甜甜圈（彩针款）',
								img: 'http://img14.360buyimg.com/n1/jfs/t1/72185/1/7121/222065/5d5377d5E46e681fa/6f100c77965b9165.jpg',
								money: '39.90',
								stock: 50
							},
							{
								goods_sku_arr: ['2022'],
								goods_sku_text: '500g甜甜圈（拉花款）',
								img: 'http://img14.360buyimg.com/n1/jfs/t1/72191/2/6973/239664/5d5377d5Ef952d7d9/606e70d2b6dd44d2.jpg',
								money: '39.90',
								stock: 50
							},
						]

					},
					{
						title: '水果3斤盲盒',
						type: 5,
						goods_id: 206,
						money: '59.90',
						number: 200,
						hmoney: '70.90',
						youhui: true,
						baoyou: true,
						img: '/static/images/goods/five.jpg',
						status: 0, //商品过期状态  0正常  1已失效
						stock: 140,
						sku: [{
							sku_id: 1,
							skuname: '种类',
							child: [{
									tagname: '3斤精品装',
									id: 2061,
									imgs: 'http://img10.360buyimg.com/n1/jfs/t1/71401/15/15968/470755/5ddb8ecaEe6a5ce65/140942226e7c7551.jpg',
									money: '59.90'
								},
								{
									tagname: '5斤精品装',
									id: 2062,
									imgs: 'http://img10.360buyimg.com/n1/jfs/t1/82339/35/16255/632261/5ddb8ecdE628ab494/cacc1d2241e9f65f.jpg',
									money: '82.90'
								},
							]
						}, ],
						skuArr: [{
								goods_sku_arr: ['2061'],
								goods_sku_text: '3斤精品装',
								img: 'http://img10.360buyimg.com/n1/jfs/t1/71401/15/15968/470755/5ddb8ecaEe6a5ce65/140942226e7c7551.jpg',
								money: '59.90',
								stock: 80
							},
							{
								goods_sku_arr: ['2062'],
								goods_sku_text: '5斤精品装',
								img: 'http://img10.360buyimg.com/n1/jfs/t1/82339/35/16255/632261/5ddb8ecdE628ab494/cacc1d2241e9f65f.jpg',
								money: '82.90',
								stock: 60
							}
						],
					}
				],
				locations: {

				},
				loading: true,
				swiperList: [{
					img: 'http://img10.360buyimg.com/n1/jfs/t1/71401/15/15968/470755/5ddb8ecaEe6a5ce65/140942226e7c7551.jpg'
				}, {
					img: '/static/images/goods/four.jpg'
				}, {
					img: 'http://img12.360buyimg.com/n1/jfs/t1/127005/26/7147/367042/5f0eb18cE9efa12ea/1a8363f7ce5a06cb.jpg'
				}],
				noticeList: [{
						id: 1,
						title: '全都吃光光'
					},
					{
						id: 2,
						title: '节约粮食'
					}
				]
			};
		},
		components: {
			headers,
			classList,
			notice,
			column,
			banner,
			hotstitle,
			recommend,
			suspension
		},
		/**
		 * 生命周期函数--监听页面加载
		 */
		onLoad: function(options) {
			// #ifdef APP-PLUS
			this.bottoms = '0'  //在APP下 规格弹窗的位置发生变化
			// #endif
		},

		/**
		 * 生命周期函数--监听页面初次渲染完成
		 */
		onReady: function() {},

		/**
		 * 生命周期函数--监听页面显示
		 */
		onShow: function() {
			this.setData({
				colors: app.globalData.newColor
			});
			uni.setNavigationBarColor({ //设置标题栏颜色
				backgroundColor: app.globalData.newColor,
				frontColor: '#ffffff'
			});
			// #ifdef H5
			let locations = getlocation() //获取位置信息
			if (locations) {
				this.locations = locations
			}
			// #endif
		},

		/**
		 * 生命周期函数--监听页面隐藏
		 */
		onHide: function() {},

		/**
		 * 生命周期函数--监听页面卸载
		 */
		onUnload: function() {},

		/**
		 * 页面相关事件处理函数--监听用户下拉动作
		 */
		onPullDownRefresh: function() {},

		/**
		 * 页面上拉触底事件的处理函数
		 */
		onReachBottom: function() {
			if (this.dataList.length >= 30) { //模拟上拉加载数据
				this.loading = false
				return
			}
			let data = this.dataList;
			setTimeout(() => {
				this.loading = true
				this.dataList.push(...data);
			}, 500)
		},

		/**
		 * 用户点击右上角分享
		 */
		onShareAppMessage: function() {},
		methods: {
			onPageScroll: function(e) {
				if (e.scrollTop >= 500) {
					this.setData({
						scrollShow: true
					});
				} else {
					this.setData({
						scrollShow: false
					});
				}
			}
		}
	};
</script>
<style scoped lang="scss">
	.home {
		margin-bottom: 40rpx;
	}
</style>
