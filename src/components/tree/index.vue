<!--
   tree 树状组件

   @param {String} data
    ex:
        {
            isHasCheckbox: true,
            leafs: [{
                isOpened: true,
                isChecked: true,
                isDisabled: true,
                content: '文本内容1'
            }, {
                content: '文本内容2',
                subTree: {
                    isHasCheckbox: true,
                    leafs: [{
                        content: '文本内容1'
                    }, {
                        content: '文本内容2'
                    }]
                }
            }]
        }
   @param {String} appendClass 自定义class
   @param {Object} appendStyle 自定义Style对象
-->

<template>
    <ul :style="appendStyle" :class="['tbd-tree', appendClass]" >
        <li v-for="it in data.leafs" :class="[{'tbd-tree-checked': it.isChecked, 'tbd-tree-disabled': it.isDisabled, 'tbd-tree-open': it.isOpened}]">
            <a href="javascript: void 0;" class="tbd-tree-item">
                <i @click.stop="toggleOpen(it)" v-if="it.subTree" class="tbd-tree-caret"></i>
                <span class="tbd-tree-text" @click.stop="toggleOpen(it)">
                    <i @click.stop="toggleChecked(it)" v-if="data.isHasCheckbox" class="tbd-tree-checkbox"></i>
                    {{it.content}}
                </span>
            </a>

            <pv-base v-if="it.subTree" :data="it.subTree" :is-parent-checked.sync="it.isChecked"></pv-base>
        </li>
    </ul>
</template>

<script>
    import {componentBaseParamConfig} from '../base-config';
    import pvBase from './_base.vue';

    export default {
        replace: false,
        components: {
            pvBase
        },
        props: Object.assign({}, componentBaseParamConfig, {
            data: {
                type: Object,
                default() {
                    return {
                        leafs: []
                    }
                }
            }
        }),
        beforeCompile: pvBase.beforeCompile,
        methods: Object.assign({}, pvBase.methods)
    }
</script>

<style scoped>
    @import "style.css";
</style>