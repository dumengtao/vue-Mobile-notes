<template>
	<div class="content" v-show="show">
		<mt-header title="记事本编辑区">
			<mt-button icon="back" slot="left" @click="showBack">返回</mt-button>
		</mt-header>
		<div v-for="(item,index) in items" v-show="showIndex === index">
			<input v-model.trim="item.title" @keyup="titleChange(index)" class="title" type="text" name="title">
			<textarea v-model.trim="item.info" class="textarea" placeholder="这里是编辑区，请您..."></textarea>
		</div>
	</div>
</template>

<script type="ecmascript-6">
	import bus from '../common/js/bus.js'
	import { Header } from 'mint-ui'

	export default {
		data() {
			return {
				showIndex: 0,
				items: [],
				show: false
			}
		},
		created() {
            // H5本地获取数据
            let data = JSON.parse(localStorage.getItem('contentData'))
            for(let i in data){
                this.items.push(data[i])
            }
            
			bus.$on('addNote',() => {
    			const t = { title: "New Note",info: '' }
    			this.items.push(t)
    		}),
			bus.$on('deleteNote',() => {
				this.items.splice(this.showIndex,1)
                if(this.showIndex > 0){
                    this.showIndex--
                }else{
                    this.showIndex = 0
                }
			}),
			bus.$on('showContent',(index) => {
				this.showIndex = index
			}),
			bus.$on('showFlag',() => {
				this.show = !this.show
			})
		},
		methods: {
			titleChange(index) {
				bus.$emit('titleChange',this.items[index].title,index)
			},
			showBack() {
				bus.$emit('showBack')
				this.show = !this.show
			}
		},
        beforeUpdate() {
            // H5本地储存数据
            localStorage.setItem('contentData',JSON.stringify(this.items))
        }
	}
</script>

<style lang="stylus" rel="stylesheet/stylus">
	.content
		box-sizing border-box
		overflow hidden
		.title
			display block
			margin 20px auto
			color #666
			font-size 26px
			text-align center
		.textarea
			width 80%
			height 450px
			border 0
			border-radius 0
			font-size 14px
			color #000
			font-family '微软雅黑'
			resize none
</style>
