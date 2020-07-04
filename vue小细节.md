## v-model双向绑定原理 
1. v-model其实是一个语法糖，它会自动的在元素或者组件上面解析为 :value="" 和 @input=""
	- `<input v-model="price"></input>`
	- `<input :value="price" @input="price=$event.target.value"></input>`
	- 拆分了一个value属性
	- 当在input输入框输入内容时，会自动的触发input事件，更新绑定的name值。
	- 当name的值通过JavaScript改变时，会更新input的value值
######
	// AddPrice.vue
	// 通过props接受绑定的value参数
	<template>
  	 	<div @click="$emit('input',value + 100 )">点击加钱<div>
		</template>
		<script>
	  	export default {
	    props: ['value']
	  	}
		</script>
		// 在父组件中调用
	<add-price v-model="price"></add-price>
	
	
	
### input的checked分为单选和多选
	- 单选的时候用true和false来进行判断是否选中就好了
	- 多选的话给他个value值然后通过v-model绑定的数组内，是否有这个value值进行判断是否选中

### element-ui 的upload组件上传图片时如果带有cookie头凭证信息需要设置属性with-credentials=true （支持发送 cookie 凭证信息）
### element-ui 的select组件v-model接收的值是一个Array类型的值，默认值也要设定为 []，不然就会报错
