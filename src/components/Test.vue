<template>
    <div class="common-layout">
        <el-container>
            <el-header>
                <el-menu :default-active="activeIndex" class="el-menu-demo" mode="horizontal" :ellipsis="false"
                    @select="handleSelect">
                    <el-menu-item index="0">
                        <img style="width: 100px" src="" alt="Element logo" />
                    </el-menu-item>
                    <div class="flex-grow" />
                    <el-menu-item index="1">Processing Center</el-menu-item>
                    <el-sub-menu index="2">
                        <template #title>Workspace</template>
                        <el-menu-item index="2-1">item one</el-menu-item>
                        <el-menu-item index="2-2">item two</el-menu-item>
                        <el-menu-item index="2-3">item three</el-menu-item>
                        <el-sub-menu index="2-4">
                            <template #title>item four</template>
                            <el-menu-item index="2-4-1">item one</el-menu-item>
                            <el-menu-item index="2-4-2">item two</el-menu-item>
                            <el-menu-item index="2-4-3">item three</el-menu-item>
                        </el-sub-menu>
                    </el-sub-menu>
                </el-menu>
            </el-header>
            <el-container>
                <el-aside width="200px" class="leftAside">
                    <el-row class="tac">
                        <el-col :span="24">
                            <!-- <h5 class="mb-2">Default colors</h5> -->
                            <el-menu default-active="2" class="el-menu-vertical-demo" @open="handleOpen"
                                @close="handleClose">
                                <el-sub-menu index="1">
                                    <template #title>
                                        <el-icon>
                                            <location />
                                        </el-icon>
                                        <span>Navigator One</span>
                                    </template>
                                    <el-menu-item-group title="Group One">
                                        <el-menu-item index="1-1">item one</el-menu-item>
                                        <el-menu-item index="1-2">item two</el-menu-item>
                                    </el-menu-item-group>
                                    <el-menu-item-group title="Group Two">
                                        <el-menu-item index="1-3">item three</el-menu-item>
                                    </el-menu-item-group>
                                    <el-sub-menu index="1-4">
                                        <template #title>item four</template>
                                        <el-menu-item index="1-4-1">item one</el-menu-item>
                                    </el-sub-menu>
                                </el-sub-menu>
                                <el-menu-item index="2">
                                    <el-icon><icon-menu /></el-icon>
                                    <span>Navigator Two</span>
                                </el-menu-item>
                                <el-menu-item index="3" disabled>
                                    <el-icon>
                                        <document />
                                    </el-icon>
                                    <span>Navigator Three</span>
                                </el-menu-item>
                                <el-menu-item index="4">
                                    <el-icon>
                                        <setting />
                                    </el-icon>
                                    <span>Navigator Four</span>
                                </el-menu-item>
                            </el-menu>
                        </el-col>
                    </el-row>
                </el-aside>
                <el-container>
                    <el-main>Main</el-main>
                    <el-footer>Footer</el-footer>
                </el-container>
            </el-container>
        </el-container>
    </div>
</template>

<script setup>
import { ref } from 'vue'
import {
    Document,
    Menu as IconMenu,
    Location,
    Setting,
} from '@element-plus/icons-vue'

const handleOpen = (key, keyPath) => {
    console.log(key, keyPath)
}
const handleClose = (key, keyPath) => {
    console.log(key, keyPath)
}

const activeIndex = ref('1')
const handleSelect = (key, keyPath) => {
    console.log(key, keyPath)
}
</script>

<style>
.flex-grow {
    flex-grow: 1;
}

.leftAside {
    height: 100vh;
}
</style>