<template>
    <el-form ref="form" :model="form" label-width="80px" class="form-contain">
        <el-form-item label="用户名">
            <el-input v-model="form.name"></el-input>
        </el-form-item>

        <el-form-item label="密码">
            <el-input v-model="form.pass"></el-input>
        </el-form-item>

        <el-form-item label="用户权限">
            <el-radio-group v-model="form.role">
                <el-radio label="1">普通用户</el-radio>
                <el-radio label="10">管理员</el-radio>
                <el-radio label="100">超级管理员</el-radio>
            </el-radio-group>
        </el-form-item>

        <el-form-item>
            <el-button type="primary" @click="onSubmit">添加用户</el-button>
            <el-button @click="onCancel">取消</el-button>
        </el-form-item>
    </el-form>
</template>

<script>
    import func from '../../public/func';
    import api from '../../public/api';

    export default {
        name: 'form',
        data() {
            return {
                form: {
                    name: '',
                    pass: '',
                    role: 0,
                }
            }
        },
        methods: {
            onSubmit () {
                if (!this.form.name) {
                    this.$message.warning('请填写完整信息');
                    return;
                }

                func.ajaxPost(api.userAdd, this.form, res => {
                    if (res.status === 201) {
                        this.$message.success('操作成功');
                        this.$router.push({name: 'user-list'});
                    }
                });
            },

            onCancel () {
                this.$router.push({name: 'user-list'});
            },

        },

    }
</script>

<style lang="scss">
    .form-contain {
        width: 50%;
        margin: 0 auto;

        .el-form-item__content {
            display: flex;
            align-items: center;
            height: 36px;
        }
    }

    .el-input-number {
        [class^='el-input-number'] {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100%;
        }
    }
</style>