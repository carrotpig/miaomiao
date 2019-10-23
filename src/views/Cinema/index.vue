<template>
    <div id="main">
        <Header />
        <div id="content">
            <div class="cinema_menu">
                <div class="city_switch">
                全城 <i class="iconfont icon-lower-triangle"></i>
                </div>
                <div class="brand_swtich">
                品牌 <i class="iconfont icon-lower-triangle"></i>
                </div>
                <div class="feature_switch">
                特色 <i class="iconfont icon-lower-triangle"></i>
                </div>
            </div>
            <cinemaList/>
        </div>
        <Tabber />
    </div>
</template>

<script type="text/ecmascript-6">
import Header from "@/components/Header";
import Tabber from "@/components/Tabber";
import cinemaList from "@/components/CinemaList";
export default {
    name:'ciname',
    data() {
    return {};
    },
    components: {
        Header,
        Tabber,
        cinemaList
    }
};
</script>

<style scoped>
#content .cinema_menu{ width: 100%; height: 45px; border-bottom:1px solid #e6e6e6; display: flex; justify-content:space-around; align-items:center; background:white;}
</style>

