<!--
  select 下拉列表
  @param {Array} data 传入组件数据,用于渲染
  @param {String} size 组件大小
  @param {String} value 绑定外部数据对象的结果
  @param {Boolean} isDisabled 当前下拉列表是否可选
  @param {Boolean} isOpened 下拉列表是否显示
  @param {Boolean} isMultiple 是否展现多选
  @param {Array} resultList 多选的结果,如果是单选时,传入无效
  @param {Boolean} hasFooter 是否展示确定取消按钮,只在多选时有效
  @param {String} okText 确定按钮的值,默认为'确定'
  @param {String} okCancel 取消按钮的值,默认为'取消'
  @param {Function} onOk 点击确定按钮后的回调函数
  @param {Function} onCancel 点击取消按钮后的回调函数
  @param {Function} onSelect 当下拉列表选中后调用,调用后会将列表隐藏
  @param {Number | String | Function} filter 传入过滤器,可以过滤下拉列表的值
  @param {Object} appendClass 自定义class
  @param {Object} appendStyle 自定义Style对象
-->
<template>
    <div :style="appendStyle"
         :class="['tbd-select', appendClass, sizeClass, {'tbd-select-disabled': isDisabled, 'tbd-dropdown-wrap-open': isOpened}]"
         @click.stop="onClick">
        <slot></slot>
        <!-- 单选 -->
        <div v-if="!isMultiple" class="tbd-dropdown" :class="{'hide': !isOpened}">
            <ul class="tbd-dropdown-menu">
                <li v-if="data.optsList.length === 0">
                    没有数据....
                </li>
                <li v-for="it in showData.optsList" value="it.value"
                    :class="['tbd-dropdown-menu-item', {'tbd-dropdown-menu-item-disabled': it.isDisabled, 'tbd-dropdown-menu-item-active': $index === curIndex}]"
                    @click.stop="onSelected($index)">
                    {{{renderLi($index)}}}
                </li>
            </ul>
        </div>
        <!-- 单选 end -->

        <!-- 多选 -->
        <div v-if="isMultiple" class="tbd-dropdown tbd-dropdown-multi" :class="{'hide': !isOpened}">
            <pv-button :type="'link'" @click.stop="onClear" :append-style="{margin: '10px'}">清除所选</pv-button>
            <pv-search :value.sync="filter" :append-style="searchAppendStyle" :size="'small'"></pv-search>
            <ul class="tbd-dropdown-menu">
                <li v-if="data.optsList.length === 0">
                    没有数据....
                </li>
                <li v-for="it in showData.optsList" value="it.value"
                    :class="['tbd-dropdown-menu-item', {'tbd-dropdown-menu-item-disabled': it.isDisabled, 'tbd-dropdown-menu-item-active': indexList.includes($index)}]"
                    @click.stop="onSelected($index, it)">
                    {{{renderLi($index)}}}
                </li>
            </ul>

            <!-- 确定取消按钮 -->
            <div v-if="hasFooter" class="tbd-dropdown-multi-footer">
                <pv-button @click.stop="_onCancel">{{cancelText}}</pv-button>
                <pv-button type='primary' @click.stop="_onOk">
                    {{okText}}
                </pv-button>
            </div><!-- 确定取消按钮 End -->
        </div>
        <!-- 多选 end -->
   </div>
</template>

<script>
import {componentBaseParamConfig} from '../base-config';
import pvSearch from '../search';
import pvButton from '../button';

export default {
    props: Object.assign({}, componentBaseParamConfig, {
        isDisabled: {
            type: Boolean,
            default: false
        },
        size: {
            type: String,
            default: 'normal'
        },
        data: {
            type: Object,
            default: {
                optsList: []
            }
        },
        value: {
        },

        onSelect: {
            type: Function
        },
        isOpened: {
            type: Boolean,
            default: false
        },
        isMultiple: {
            type: Boolean,
            default: false
        },
        resultList: {
            type: Array,
            default() {
                return [];
            }
        },
        hasFooter: {
            type: Boolean,
            default: true
        },

        okText: {
            type: String,
            default: '确定'
        },

        cancelText: {
            type: String,
            default: '取消'
        },

        onOk: {
            type: Function
        },

        onCancel: {
            type: Function
        },
        filter: {}
    }),

    data () {
        let _this = this;
        return {
            curIndex: (function() {
                return _this.data.optsList.findIndex(function(it) {
                    return it.value == _this.value;
                });
            })(),
            // 多选,记录哪些选项呗选中的index
            indexList: [],
            // 临时存选择结果,为了确定和取消
            resultListTemp: Array.from(this.resultList),
            // search 样式控制
            searchAppendStyle: {
                float: 'right',
                margin: '10px 10px 5px 0',
                width: '200px'
            }
        }
    },

    computed: {
        sizeClass() {
            const sizeMap = {
                'normal': '',
                'large': 'tbd-switch-lg',
                'small': 'tbd-switch-sm"'
            };

            return sizeMap[this.size]
        },

        showData() {
            var _this = this;

            if(!this.filter) return this.data;
            if(Object.prototype.toString.call(this.filter) === '[object Function]') {
                return {
                    optsList: this.filter(this.data)
                };
            } else {
                return {
                    optsList: (this.filter === '' || this.filter === '请选择') ? this.data.optsList : this.data.optsList.filter((it) => {return it.label && it.label.includes(_this.filter)})
                };
            }
        }
    },

    methods: {
        onClick() {
            if(this.isDisabled) return;

            this.isOpened = true;
        },

        onSelected (index, item){
            let opts = this.showData.optsList;

            if(opts[index].isDisabled) return;

            // 多选
            if(this.isMultiple) {
                if(!this.indexList.includes(index)) {
                    this.resultListTemp.push(opts[index]);
                    this.indexList.push(index);
                } else {
                    this.indexList.$remove(index);
                    const existIndex = this.resultListTemp.findIndex((it) => {return it.value === opts[index].value});
                    if(existIndex >= 0)  {
                        this.resultListTemp.splice(existIndex, 1);
                    }
                    this.resultListTemp.$remove(item);
                }
            } else {
                this.value = opts[index].value;
                this.isOpened = false;
                this.onSelect && this.onSelect(index, opts[index]);
                this.curIndex = index;
            }


        },

        renderLi(index) {
            let opts = this.showData.optsList;
            let curObj = opts[index];

            if(curObj.renderLi && typeof curObj.renderLi == 'function') {
                return curObj.renderLi(index, opts[index]);
            } else {
                return curObj.label || curObj.value;
            }
        },

        _onOk() {
            this.resultList = Array.from(this.resultListTemp);
            this.onOk && this.onOk();
            this.isOpened = false;
        },

        _onCancel() {
            this.resultListTemp = Array.from(this.resultList);
            this.onCancel && this.onCancel();
            this.isOpened = false;
        },

        onClear() {
            this.resultListTemp.splice(0);
            this.indexList.splice(0);
        }
    },

    ready() {
        let _this = this;

        document.addEventListener('click', function() {
            _this.isOpened = false
        });
    },

    watch: {
        isOpened() {
            this.indexList = (() => {
                let res = [];
                    this.data.optsList.map((it, index) => {
                        if(this.resultList.find((el) => {
                        return el.value == it.value;
                })) {
                        res.push(index);
                    }
                });

                return res;
            })()
        }
    },

    components: {
        pvButton,
        pvSearch
    }
}
</script>

<style scoped>
    @import "style.css";
</style>