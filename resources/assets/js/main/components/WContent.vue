<template>
    <div class="w-content" :style="`background-image:${getBgUrl(bgid)}`">
        <slot/>
    </div>
</template>

<style lang="scss" scoped>
    .w-content {
        position: absolute;
        top: 72px;
        left: 0;
        right: 0;
        bottom: 0;
        overflow: auto;
        background-repeat: no-repeat;
        background-position: center;
        background-color: #EEEEEE;
        background-size: cover;

        .w-container {
            min-height: 500px;
        }
    }
</style>
<script>
    export default {
        name: 'WContent',
        data() {
            return {
                bgid: -1,
            }
        },
        mounted() {
            this.bgid = $A.runNum(this.usrInfo.bgid);
        },
        watch: {
            usrInfo: {
                handler(info) {
                    this.bgid = $A.runNum(info.bgid);
                },
                deep: true
            }
        },
        methods: {
            getBgUrl(id, thumb) {
                if (id < 0) {
                    return 'none';
                }
                id = Math.max(1, parseInt(id));
                return 'url(' + window.location.origin + '/images/bg/' + (thumb ? 'thumb/' : '') + id + '.jpg' + ')';
            },
        }
    }
</script>
