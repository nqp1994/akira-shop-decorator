<template>
    <div class="common-search-bar-property">
        <el-tabs v-model="activeName" stretch>
            <el-tab-pane label="搜索框" name="bar">
                <el-form>
                    <el-form-item label="提示文字">
                        <el-input maxlength="20" v-model="property.bar.placeholder"
                                  @input="onPropertyChange()"></el-input>
                    </el-form-item>
                    <el-row :gutter="20">
                        <el-col :span="8">
                            <el-form-item label="背景">
                                <theme-color-picker v-model="property.bar.bgColor"
                                                    @change="onPropertyChange"></theme-color-picker>
                            </el-form-item>
                        </el-col>
                        <el-col :span="8">
                            <el-form-item label="图标">
                                <colorUI-icon-selector @change="onPropertyChange"
                                                       v-model="property.bar.icon"></colorUI-icon-selector>
                            </el-form-item>
                        </el-col>
                        <el-col :span="8">
                            <el-form-item label="圆角">
                                <el-switch v-model="property.bar.round"
                                           @change="onPropertyChange()"></el-switch>
                            </el-form-item>
                        </el-col>
                    </el-row>
                </el-form>
            </el-tab-pane>
            <el-tab-pane label="搜索按钮" name="button">
                <common-colorUI-button :property="property.button"
                                                  @propertyChange="onPropertyChange('button','',$event)"></common-colorUI-button>
            </el-tab-pane>
        </el-tabs>
    </div>
</template>

<script>
    export default {
        name: "search-bar-common-panel",
        props: {
            property: {
                type: Object
            }
        },
        data() {
            return {
                activeName: 'bar'
            }
        },
        methods: {
            onPropertyChange(prop, type, e) {
                if (prop === 'button') {
                    this.property.button = e

                } else {
                    if (type === 'icon') {
                        this.property.bar.icon = e.name
                    }
                }

                this.$emit('propertyChange', {
                    name: this.$options.name,
                    data: this.property
                })
            }
        }
    }
</script>

<style scoped>
    .common-search-bar-property {
        text-align: initial;
    }
</style>
