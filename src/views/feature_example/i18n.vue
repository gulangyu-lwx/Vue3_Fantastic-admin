<i18n>
{
    "zh-cn": {
        "intro": "除了支持全局多语言切换，还支持 Vue 单文件模式语言切换，你可以尝试在这个页面点击右上角的语言切换试试"
    },
    "zh-tw": {
        "intro": "除了支持全局多語言切換，還支持 Vue 單文件模式語言切換，你可以嘗試在這個頁面點擊右上角的語言切換試試"
    },
    "en": {
        "intro": "In addition to global multi-language switch, also support Vue single file mode language switch, you can try to click on the top right corner of the page to switch language"
    }
}
</i18n>

<template>
    <div>
        <page-header :title="$t('route.i18n')" :content="$t('intro')" />
        <page-main title="Element 组件">
            <el-pagination :current-page="page" :page-sizes="[100, 200, 300, 400]" :page-size="pageSize" layout="total, sizes, prev, pager, next, jumper" :total="400" @size-change="handleSizeChange" @current-change="handleCurrentChange" />
        </page-main>
    </div>
</template>

<script>
export default {
    data() {
        return {
            page: 1,
            pageSize: 100
        }
    },
    methods: {
        handleSizeChange(val) {
            this.pageSize = val
            console.log(`每页 ${val} 条`)
        },
        handleCurrentChange(val) {
            this.page = val
            console.log(`当前页: ${val}`)
        }
    }
}
</script>
