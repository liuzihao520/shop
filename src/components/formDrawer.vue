<template>
    <el-drawer v-model="showDrawer" :title="title" :size="size" :close-on-click-modal="false"
        :destroy-on-close="destroyOnClose">
        <div class="formDrawer">
            <div class="body">
                <slot>

                </slot>
            </div>

            <div class="actions">
                <el-button type="primary" :loading="loading" @click="submit"> {{ confirmText }}</el-button>
                <el-button type="defalut" @click="close">取 消</el-button>
            </div>
        </div>
    </el-drawer>
</template>

<script setup>
import { ref } from "vue"
const showDrawer = ref(false)
const props = defineProps({
    title: String,
    size: {
        type: String,
        default: "45%"
    },
    destroyOnClose: {
        type: Boolean,
        default: "false"
    },
    confirmText: {
        type: String,
        default: "提交"
    }
})
//加载状态
const loading = ref(false)
const showloading = () => loading.value = true
const hideloading = () => loading.value = false

//打开
const open = () => showDrawer.value = true

//关闭 
const close = () => showDrawer.value = false

//提交
const emit = defineEmits(["submit"])
const submit = () => emit("submit")


//向父组件暴露以下方式
defineExpose({
    open,
    close,
    showloading,
    hideloading,
})
</script>

<style>
.formDrawer {
    width: 100%;
    height: 100%;
    position: relative;
    @apply flex flex-col;
}

.formDrawer .body {
    flex: 1;
    height: 100%;
    overflow-y: auto;
}

.formDrawer .actions {
    height: 50px;
    @apply mt-auto flex items-center;
}
</style>