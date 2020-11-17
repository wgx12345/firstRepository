<template>
    <div id="app">
        <router-view></router-view>
    </div>
</template>
<script>
import store from './vuex/store'
import {SET_BASEINFO,GET_BASEINFO} from './mutaion_types'
export default {
    store,
    name: 'app',
    data(){
        return {
            user_info: {
                open_id: this.$route.query.open_id
            }
        }
    },
    mounted () {
        //TODO开发环境下使用，生产环境下注释
        //store.dispatch(SET_BASEINFO,{open_id: 'opFELv6YkJkMaH-xFkokTWCs5A1Q'})

        if(this.user_info.open_id){
            store.dispatch(SET_BASEINFO,this.user_info)
        }else{
            stroe.dispatch(SET_BASEINFO)
            if(store.state.userInfo.open_id === undefined){
                console.info('用户id和open_id不存在，跳转到授权等待页面')
                this.$router.push({name: 'wait_to_shouquan'})
            }else{
                console.info('已经有BASEINFO')
            }
        }
    },
    watch: {
        '$route' (val){

        }
    },
    methods: {

    },
    components: {
        
    }
    
}
</script>