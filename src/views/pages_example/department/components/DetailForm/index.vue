<template>
    <div v-loading="data.loading">
        <el-form ref="form" :model="data.form" :rules="data.rules" label-width="120px" label-suffix="：">
            <el-form-item label="部门" prop="title">
                <el-input v-model="data.form.title" placeholder="请输入部门名称" />
            </el-form-item>
        </el-form>
    </div>
</template>

<script setup>
const { proxy } = getCurrentInstance()

const props = defineProps({
    id: {
        type: [Number, String],
        default: ''
    }
})

const data = ref({
    loading: false,
    form: {
        id: props.id,
        title: ''
    },
    rules: {
        title: [
            { required: true, message: '请输入部门名称', trigger: 'blur' }
        ]
    }
})

onMounted(() => {
    if (data.value.form.id != '') {
        getInfo()
    }
})

function getInfo() {
    data.value.loading = true
    proxy.$api.get('pages_example/department/detail', {
        baseURL: '/mock/',
        params: {
            id: data.value.form.id
        }
    }).then(res => {
        data.value.loading = false
        data.value.form.title = res.data.title
    })
}

defineExpose({
    submit(callback) {
        if (data.value.form.id == '') {
            proxy.$refs['form'].validate(valid => {
                if (valid) {
                    proxy.$api.post('pages_example/department/create', data.value.form, {
                        baseURL: '/mock/'
                    }).then(() => {
                        proxy.$message.success({
                            message: '模拟新增成功',
                            center: true
                        })
                        callback && callback()
                    })
                }
            })
        } else {
            proxy.$refs['form'].validate(valid => {
                if (valid) {
                    proxy.$api.post('pages_example/department/edit', data.value.form, {
                        baseURL: '/mock/'
                    }).then(() => {
                        proxy.$message.success({
                            message: '模拟编辑成功',
                            center: true
                        })
                        callback && callback()
                    })
                }
            })
        }
    }
})
</script>

<style lang="scss" scoped>
// scss
</style>
