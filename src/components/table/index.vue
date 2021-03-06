<!--
   table 组件

   @param {Array} data 用于table tbody部分的数据渲染
   ex:
          data: [{
            key: 0,
            name: 'name0',
            age: 32,
            address: 'address0'
          }, {
            key: 1,
            name: 'name1',
            age: 33,
            address: 'address1'
          }]


   @param {Array} columns 用于table thead部分的渲染,并可以通过传入rander函数对数据进行渲染指定
   ex:
           columns: [{
                        title: '姓名',
                        dataIndex: 'name',
                        render(text, item) {
                          return `<a href="#">${text}</a>`;
                        }
                      }, {
                        title: '年龄',
                        dataIndex: 'age'
                      }, {
                        title: '住址',
                        dataIndex: 'address'
                      }, {
                        title: '操作',
                        render(text, item) {
                          return `<a class="tbd-inline" @click="clickOperate">操作一</a>
                                    <span class="tbd-divider"></span>
                                  <a class="tbd-inline">操作二</a>`;
                        }
                    }]
   @param {Function} onChangePage 用于传入分页组件页面变更事件进行响应
   @param {Number} currentPage 当前组件停留页
   @param {Number} pageSize 总页数
   @param {Boolean} isShowPagination 是否显示分页栏
   @param {String} appendClass 自定义class
   @param {Object} appendClass 自定义Style对象
-->
<template>
    <div class="tbd-table">
        <div class="tbd-table-body">
            <table>
                <thead>
                    <tr>
                        <th v-for="col in cols">{{col.title}}</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="row in currentData" track-by="$index">
                        <td v-for="col in cols">{{{renderTD(col, row)}}}</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>

    <pv-pagination :total="totalNum" :current-page.sync="currentPage" :page-size.sync="pageSize" :on-change="onChangePage"></pv-pagination>
</template>

<script>
    import pvPagination from '../pagination'

    export default {
        props: {
            data: {
                type: Array
            },

            columns: {
                type: Array
            },

            onChangePage: {
                type: Function,
                default: function(index) {}
            },

            currentPage: {
                type: Number,
                default: 1
            },

            pageSize: {
                type: Number,
                default: 5
            },

            total: {
                type: Number
            },

            isShowPagination: {
                type: Boolean,
                default: true
            }
        },

        data () {
            return {

            }
        },

        watch: {
            data: function(val, newVal) {
                // 表格数据变化 分页重置为默认
                this.currentPage = 1;
                this.pageSize = 5;
            }
        },

        components: {
            pvPagination
        },

        computed: {
            // 计算表头,如果没有传入表头,使用data数据的第一行进行绘制
            cols () {
                if (this.columns !== undefined) {
                    return this.columns
                }

                let cols = [];

                this.data[0] && (cols = Object.keys(this.data[0]).map((col) => {
                            return {
                                dataIndex: col,
                                title: col
                            }
                        }));

                return cols;
            },

            // 展示数据
            currentData() {
                // 取出当前页数据
                if (this.data && this.data.length > 0) {
                    return this.data.slice(this.pageSize *
                            (this.currentPage - 1), this.pageSize * this.currentPage)
                }

                return []
            },

            totalNum () {
                // 真分页时
                if (this.total !== undefined) {
                    return this.total
                }

                // 非真分页时
                if (this.data && this.data.length > 0) {
                    return this.data.length
                }

                return 0
            },

            // 根据传入的渲染函数,对列进行渲染
            renderTD() {
                return (col, row) => {
                    if (col.render && typeof col.render === 'function') {
                        return col.render(row[col.dataIndex], row)
                    } else {
                        return row[col.dataIndex]
                    }
                }

            }
        }
    }
</script>

<style scoped>
    @import "style.css";
</style>