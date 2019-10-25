<template>
	<div class="city_body">
		<div class="city_list">
			<div class="city_hot">
				<h2>热门城市</h2>
				<ul class="clearfix">
				<li v-for="(item, index) in hotlist" :key="index">{{item.nm}}</li>
				</ul>
			</div>
			<div class="city_sort" ref="city_sort">
				<div v-for="(item, index) in cityList" :key="index">
				<h2>{{item.index}}</h2>
				<ul>
					<li v-for="(element, index) in item.list" :key="index">{{element.nm}}</li>
				</ul>
				</div>
			</div>
		</div>
		<div class="city_index">
		<ul>
			<li v-for="(item, index) in cityList" :key="index"  @touchstart="handleToIndex(index)">{{item.index}}</li>
		</ul>
		</div>
	</div>

</template>

<script type="text/ecmascript-6">
export default {
	name: "city",
		data() {
			return {
				cityList:[],
				hotlist:[]
			};
		},
	mounted() {
		this.axios.get('/api/cityList').then((res)=>{
			var msg = res.data.msg
			if(msg === 'ok'){
				var cities = res.data.data.cities
				// 获得的对象类型为{[{index:'A',list:['aa','aa']}]}
				var {cityList,hotlist} = this.getCityList(cities)
				this.cityList = cityList
				this.hotlist = hotlist
			}
			
		})
	},
	methods: {
		getCityList:function(cities){
			var cityList = []
			var hotlist = []

			//获取热门城市
			for (let i = 0; i < cities.length; i++) {
				if(cities[i].isHot){
					hotlist.push(cities[i])
				}
			}
			//获取城市排序列表
			for (let i = 0; i < cities.length; i++) {
				var firstLetter = cities[i].py.substring(0,1).toUpperCase()
				if(toCom(firstLetter)){   //新增
					cityList.push({index:firstLetter,list:[{nm:cities[i].nm,id:cities[i].id}]})
				}else{		//追加
					for (let j = 0; j < cityList.length; j++) {
						if(cityList[j].index === firstLetter){
							cityList[j].list.push({nm:cities[i].nm,id:cities[i].id})
						}
						
					}
				}
			}
			function toCom(firstLetter) {
				for (let i = 0; i < cityList.length; i++) {
					if(cityList[i].index === firstLetter){
						return false
					}
				}
				return true
			}
			//按字母排序
			cityList.sort((n1,n2)=>{
				if(n1.index > n2.index){
					return 1
				}else if (n1.index < n2.index){
					return -1
				}else{
					return 0
				}
			})
			return{
				cityList,
				hotlist
			}
		},
		handleToIndex(index){
			var h2 = this.$refs.city_sort.getElementsByTagName('h2')
			this.$refs.city_sort.parentNode.scrollTop=h2[index].offsetTop
			console.log(this.$refs.city_sort.parentNode);
			console.log(h2[index].offsetTop);
			console.log(index);
			
		}
	},
	components: {}
};
</script>

<style scoped>
#content .city_body {
	margin-top: 45px;
	display: flex;
	width: 100%;
	position: absolute;
	top: 0;
	bottom: 0;
}
.city_body .city_list {
	flex: 1;
	overflow: auto;
	background: #fff5f0;
}
.city_body .city_list::-webkit-scrollbar {
	background-color: transparent;
	width: 0;
}
.city_body .city_hot {
	margin-top: 20px;
}
.city_body .city_hot h2 {
	padding-left: 15px;
	line-height: 30px;
	font-size: 14px;
	background: #f0f0f0;
	font-weight: normal;
}
.city_body .city_hot ul li {
	float: left;
	background: #fff;
	width: 29%;
	height: 33px;
	margin-top: 15px;
	margin-left: 3%;
	padding: 0 4px;
	border: 1px solid #e6e6e6;
	border-radius: 3px;
	line-height: 33px;
	text-align: center;
	box-sizing: border-box;
	}
	.city_body .city_sort div {
	margin-top: 20px;
	}
	.city_body .city_sort h2 {
	padding-left: 15px;
	line-height: 30px;
	font-size: 14px;
	background: #f0f0f0;
	font-weight: normal;
}
.city_body .city_sort ul {
	padding-left: 10px;
	margin-top: 10px;
}
.city_body .city_sort ul li {
	line-height: 30px;
	line-height: 30px;
}
.city_body .city_index {
	width: 20px;
	display: flex;
	flex-direction: column;
	justify-content: center;
	text-align: center;
	border-left: 1px #e6e6e6 solid;
}
</style>
