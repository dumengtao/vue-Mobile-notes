<template>
    <div class="select" v-show="show">
    	<div class="add" @click="addNote()"><i class="icon-plus"></i></div>
    	<div class="collect" @click="favNote()"><i class="icon-star-full"></i></div>
    	<div class="delete" @click="deleteNote()"><i class="icon-cross"></i></div>
    </div>
</template>

<script type="ecmascript-6">
	import bus from '../common/js/bus.js'
    import { Toast } from 'mint-ui'
    import { MessageBox } from 'mint-ui'

    export default {
        data() {
            return {
                show: true
            }
        },
        created() {
            bus.$on('showFlag',() => {
                this.show = !this.show
            }),
            bus.$on('showBack',() =>{
                this.show = !this.show
            })
        },
    	methods: {
    		addNote() {
                bus.$emit('addNote')
                Toast({
                    message: '恭喜您，成功添加新笔记!',
                    duration: 1000
                })
    		},
    		favNote() {
    			bus.$emit('favNote')
    		},
    		deleteNote() {
                MessageBox.confirm('是否删除该笔记?').then(action => {
                    bus.$emit('deleteNote')
                    Toast({
                        message: '删除成功!',
                        duration: 1000
                    })
                }).catch(action => {
                    Toast({
                        message: '已取消删除!',
                        duration: 1000
                    })
                })
    		}
    	}
    }
</script>

<style lang="stylus" rel="stylesheet/stylus">
    .select
        box-sizing border-box
        width 100%
        height 36px
        background-color #337ab7
        color #B9ACAC
        .add,.collect,.delete
            float left
            width 33%
            height 36px
            cursor pointer
            .icon-plus,.icon-cross
                opacity .8
                font-size 25px
                line-height 36px
            .icon-star-full
                opacity .8
                font-size 30px
                line-height 36px
                &.fav
                    color #F7AE4F
        .delete
            margin-top 2px
</style>
