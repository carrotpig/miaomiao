<template>
    <div id="main">
        <Header />
            <div id="content">
                <Login />
            </div>
        <Tabber />
    </div>
</template>

<script type="text/ecmascript-6">
import Header from '@/components/Header'
import Tabber from '@/components/Tabber'
import Login from '@/components/Login'
export default {
    data() {
        return {

        }
    },
    components: {
        Header,
        Tabber,
        Login
    }
}
</script>

<style scoped lang="stylus" scoped>
</style>

