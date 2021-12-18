<template>
	<div id="myChart" style="height:100%;width:100%;"></div>
</template>

<script>
	import echarts from 'echarts'
	
	export default {
		data() {
			return {

			}
		},
		mounted() {
			this.draw()
		},
		methods: {
			draw() {
				//初始化echarts实例
				let myChart = this.$echarts.init(document.getElementById('myChart'))
				//绘制图表
				var option = {

					title: {
						text: ' '
					},
					grid:{//同radar里的center[]
						position:"center"
					},
					tooltip:{
						confine:true,
						enterable:true //鼠标是否可以移动到tooltip区域内
					},
					//多个线条时，使用时name:'图一'区分
//					legend: {
//						data: ['图一', '图二']
//					},
					radar: {
							center: ['50%', '57%'],//调位置
							radius: 80,//调大小
							startAngle: 90,
							splitNumber: 4,//雷达图圈数设置
							//雷达图形状圆形    	shape:'circle',
							name: {
								formatter: '【{value}】',
								textStyle: {
									color: '#72ACD1',
									fontWeight: 'bold'
								}
							},
							//雷达图的指示器，指定雷达图的多个维度
							indicator: [{
									text: '知识数量',
									max: 100
								},
								{
									text: '租户数',
									max: 100
								},
								{
									text: '发布次数',
									max: 100
								},
								{
									text: '实例数',
									max: 100
								},
								{
									text: '算法服务数量',
									max: 100
								}
							],
							
							splitArea: {
								show:true,
								areaStyle: {
									color: ['rgba(114, 172, 209, 1)',//图表背景颜色
									]
								}
							},
							splitLine: {
								show:true,
								lineStyle: {
									width:1,
									color: 'rgba(255, 255, 255, 1)'//网格颜色
								}
							},
							//雷达图中间射线的颜色
							axisLine: {
								lineStyle: {
									color: 'rgba(255, 255, 255, 1)'
								}
							},
							
						},
					
					series: [{
							name: '雷达图',
							type: 'radar',
							symbol: 'circle',//拐点样式
							symbolSize:6,//拐点大小
							areaStyle:{  //拐点颜色
								narmal:{
									width:1,
									opacity:0.2,
									color:'#0184BB'
								}
							},
							data: [{
								//设置各个指标的值
									value: [34, 8,67, 28, 17],
//									name: '图一', 
									//让数值在拐点处显示
                                    label:{
                                    	show:true,
                                    	formatter:function(params){
                                    		return params.value
                                    	}
                                    },
                                    //设置区域边框和区域的颜色
									itemStyle:{
										normal:{
											color:'rgba(255, 255, 0, 1)',
											lineStyle:{
												color:'rgba(255, 255, 0, 1)'
											}
										}
									}
							},
							]
					},
					]
				}
				//防止越界，重绘echarts（例如屏幕缩小，图标随屏幕适应）
				window.onresize = myChart.resize;
				myChart.setOption(option);; //设置option
			}
		}
	}
</script>

<style scoped="scoped">
	#myChart{
		display: flex;
        align-items: center;
        justify-content: center;
	}
</style>
