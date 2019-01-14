<template>
    </myBreadcrumb>
    <div class="user-container">
        <!-- 顶部面包屑 -->
        <el-row>
            <el-col :span="24">
                <div class="grid-content bg-purple-dark">
                    <myBreadcrumb level2="牛逼" level3="真牛逼">
                </div>
            </el-col>
        </el-row>
        <!-- 操纵框 -->
        <el-row>
            <el-col :span="8">
                <div class="grid-content bg-purple-dark">
                    <el-input placeholder="请输入内容" v-model="input4">
                        <template slot="append">
                                <el-button icon="el-icon-search" circle></el-button>
                                </template>
                        </el-input>

                </div>
            </el-col>
             <el-col :span="3">
                <div class="grid-content bg-purple-dark">
                     <el-button type="success">成功按钮</el-button>

                </div>
            </el-col>
            
        </el-row>
    </div>
</template>
<script>
    export default {
        data() {
            return {
                level2:"用户管理",
                level3:"用户列表"
            };
        },
    };
</script>
<style>
.user-container {
    background-color: aqua;
    padding-left: 20px;
}
</style>
