<template>
  <div class="doc-header">
    <div class="inner">
      <ul class="nav">
        <li class="current"><a href="index.html">首页</a></li>
      </ul>
    </div>
  </div>
  <!-- text body-->
  <div class="doc-index doc-container">
    <section class="doc-main">
      <h2>基本元素</h2>

      <div class="doc-example">
        <section class="doc-part">
          <h3>button:</h3>
          <v-button>default</v-button>
          <v-button type="primary" size="large" @click="buttonClick()">primary/large</v-button>
          <v-button type="outline">outline</v-button>
          <v-button type="error">error</v-button>
          <v-button type="link" size="small" >link/small</v-button>
          <v-button type="primary" :is-disabled="true" @click="buttonClick()">primary/disable</v-button>
          <!-- 带图标 -->
          <h3>带图标button:</h3>
          <v-button>
            <span>default</span>
            <span class="tbdi tbdi-down"></span>
          </v-button>
          <v-button>
            <span class="tbdi tbdi-down"></span>
            <span>default</span>
          </v-button>
        </section>

        <section class="doc-part">
          <h2>按钮组</h2>
          <v-button-group :data="buttonGroupList"></v-button-group>
        </section>


        <!-- switch -->
        <section class="doc-part">
          <h3>switch: {{switchValue}}</h3>
          <v-switch :value.sync="switchValue" :onChange="switchChange"></v-switch>
        </section>

        <!-- checkbox -->
        <section class="doc-part">
          <h3>checkbox: 横向{{checkboxResultList | json}}</h3>
          <v-checkbox :data="commonListData" :result-list.sync="checkboxResultList"></v-checkbox>
          <h3>checkbox: 纵向{{checkboxResultList | json}}</h3>
          <v-checkbox :data="commonListData" :result-list.sync="checkboxResultList" :is-vertical="true"></v-checkbox>
        </section>

        <!-- radio -->
        <section class="doc-part">
          <h3>radio: 横向{{radioResultList | json}}</h3>
          <v-radio :data="commonListData" :result-list.sync="radioResultList"></v-radio>
          <h3>radio: 纵向/多选{{radioMulResultList | json}}</h3>
          <v-radio :data="commonListData" :result-list.sync="radioMulResultList" :is-vertical="true" :is-multiple="true"></v-radio>
        </section>

        <!-- select -->
        <section class="doc-part">
          <h3>select: {{dropDownValue}}</h3>
          <v-select :data="dropDownData" :append-style="{width: '200px'}" :value.sync="dropDownValue"></v-select>
          <v-select :data="dropDownData" :is-disabled="true" :value.sync="dropDownValue"></v-select>
        </section>
      </div>

      <h2>下拉列表(未完成)</h2>
      <div class="doc-example">
        <section class="doc-part">
          <h3>dropdown单选: {{dropDownValue}}</h3>
          <v-select :data="dropDownData" :append-style="{width: '200px'}" :value.sync="dropDownValue"></v-select>
          <h3>dropdown多选: {{multiResList | json}}</h3>
          <v-multi-select :data="multiDataList" :append-style="{width: '200px'}" :result-list.sync="multiResList"></v-multi-select>
        </section>
      </div>

      <h2>弹窗</h2>
      <div class="doc-example">
        <h3>tips类弹窗</h3>
        <section class="doc-part">
          <v-tips :id="'infoTips1'" :content="'我是一个提示操作/类型是info'" type="info"></v-tips>
          <v-tips :id="'infoTips2'" :content="'我是一个提示操作/类型是success'" type="success"></v-tips>
          <v-tips :id="'infoTips3'" :content="'我是一个提示操作/类型是error'" type="error"></v-tips>
          <v-tips :id="'infoTips4'" :content="'我是一个提示操作/类型是warn'" type="warn"></v-tips>

          <!-- 第一种调用方法 -->
          <v-button type="primary" @click="showTips('infoTips1', 'info')">tips info</v-button>
          <v-button type="primary" @click="showTips('infoTips2', 'success')">tips success</v-button>
          <v-button type="primary" @click="showTips('infoTips3', 'error')">tips error</v-button>
          <v-button type="primary" @click="showTips('infoTips4', 'warn')">tips warn</v-button>

          <!-- 第二种调用方法 -->
          <v-button @click="showTipsWay2()">tips info 第二种调用方法</v-button>
        </section>

        <h3>messageBox类弹窗</h3>
        <section class="doc-part">
          <v-message-box :id="'mb1'" type="info" :title="'这是一条通知信息'" :explain="'一些解释'" :on-ok="dialogCallbackFn1"></v-message-box>
          <v-message-box :id="'mb2'" type="success" :title="'这是一条通知信息'" :explain="'一些解释'"></v-message-box>
          <v-message-box :id="'mb3'" type="error" :title="'这是一条通知信息'" :explain="'一些解释'"></v-message-box>
          <v-message-box :id="'mb4'" type="confirm" :title="'您是否确认要删除这项内容'" :explain="'一些解释'" :on-cancel="dialogCallbackFn1"></v-message-box>

          <v-button type="primary" @click="showMb('mb1', 'info')">msgBox info</v-button>
          <v-button type="primary" @click="showMb('mb2', 'success')">msgBox success</v-button>
          <v-button type="primary" @click="showMb('mb3', 'error')">msgBox error</v-button>
          <v-button type="primary" @click="showMb('mb4', 'confirm')">msgBox confirm</v-button>
        </section>

        <h3>dialog类弹窗</h3>
        <section class="doc-part">
          <v-dialog :id="'dialog1'" :on-ok="dialogCallbackFn1" :on-cancel="dialogCallbackFn2">
            <div>hi, 我是一个弹窗</div>
            <div>hi, 我是一个弹窗</div>
            <div>hi, 我是一个弹窗</div>
            <div>hi, 我是一个弹窗</div>
          </v-dialog>

          <v-button type="primary" @click="showDialog('dialog1')">show dialog</v-button>
        </section>

      </div>

      <h2>tabs</h2>
      <div class="doc-example">
        <h2>默认类型tabs</h2>
        <v-tabs type="" :on-change="switchChange">
          <div slot="operate">
            <v-button>额外操作</v-button>
          </div>

          <div slot="header">
            <div class="a">
              <i class="tbdi tbdi-apple"></i>
              <span>选项卡1</span>
            </div>
            <div>选项卡2</div>
            <div>选项卡3</div>
          </div>

          <v-pane>选项卡111111内容</v-pane>
          <v-pane>选项卡222222内容</v-pane>
          <v-pane>选项卡33333内容</v-pane>
        </v-tabs>

        <h2>card tabs</h2>
        <v-tabs type="card" :active-index="activeIndex">
          <div slot="header">
            <div class="a">选项卡1</div>
            <div>选项卡2</div>
            <div>选项卡3</div>
          </div>

          <v-pane>选项卡111111内容</v-pane>
          <v-pane>选项卡222222内容</v-pane>
          <v-pane>选项卡33333内容</v-pane>
        </v-tabs>

        <h2>panel tabs small</h2>
        <v-tabs type="panel" size="small" :active-index="1">
          <div slot="header">
            <div class="a">选项卡1</div>
            <div>选项卡2</div>
            <div>选项卡3</div>
          </div>

          <v-pane>选项卡111111内容</v-pane>
          <v-pane>选项卡222222内容</v-pane>
          <v-pane>选项卡33333内容</v-pane>
        </v-tabs>

        <h2>panel tabs small</h2>
        <v-tabs type="panel" size="large">
          <div slot="header">
            <div class="a">选项卡1</div>
            <div>选项卡2</div>
            <div>选项卡3</div>
          </div>

          <v-pane>选项卡111111内容</v-pane>
          <v-pane>选项卡222222内容</v-pane>
          <v-pane>选项卡33333内容</v-pane>
        </v-tabs>
      </div>

      <!-- 以下为未来得及重构的组件 -->
      <h2>表格</h2>
      <div class="doc-example">
        <h2>普通表格</h2>
        <v-table :data="table.data" :columns="table.columns"></v-table>
      </div>

      <h2>滑动输入条</h2>
      <div class="doc-example">
        <div style="left: 10px; top: 200px; width: 400px;">
          <v-slider min="100" max="1000" :value.sync="sliderValue" :text="'px'"></v-slider>
        </div>
        <input type="text" style="margin-top:20px;" v-model="sliderValue"></input>
        <div style="left: 10px; top: 200px; width: 400px;">
          <v-slider :value.sync="sliderValue2" :text="'px'" :value-list="sliderValueList"></v-slider>
        </div>
        <input type="text" style="margin-top:20px;" v-model="sliderValue2"></input>
      </div>

      <h2>警告提示组件</h2>
      <div class="doc-example">
        <v-alert :id="'alert1'" :title="'我是标题'" :explain="'辅助说明性文字'" :type="'success'"></v-alert>
        <v-alert :id="'alert2'" :title="'我是标题'" :explain="'辅助说明性文字'" :type="'error'" :is-close-able="true"></v-alert>

        <v-button type="primary" @click="showAlert('alert1')">alert success</v-button>
        <v-button type="primary" @click="showAlert('alert2')">alert error</v-button>
      </div>

      <h2>徽标数</h2>
      <h2>徽标数</h2>
      <div class="doc-example">
        <v-badge :number="10" :is-show-number="true">
          <i class="tbdi tbdi-mail"></i>
        </v-badge>
        <v-badge style="margin-left: 30px;">
          <i class="tbdi tbdi-mail"></i>
        </v-badge>
      </div>

      <h2>输入框和文本域</h2>
      <div class="doc-example">
        <v-input type="text" size="small" placeholder="sm"></v-input>
        <v-input type="text" value="disabled" disabled></v-input>

        <v-textarea rows="3" placeholder="textarea的高度由rows属性决定"></v-textarea>
        <v-textarea rows="3" placeholder="textarea的高度由rows属性决定" disabled></v-textarea>
      </div>

      <h2>折叠面板</h2>
      <div class="doc-example">
        <v-collapse :title="'我是一个下拉面板'">
          <div slot="operate">
            <a href="" class="tbd-link">额外操作</a>
          </div>
          <div style="padding: 20px 0;">
            <p>内容内容</p>
          </div>
        </v-collapse>
      </div>

      <h2>折叠面板组</h2>
      <div class="doc-example">
        <v-collapse-group :is-multiple="false">
          <!-- xx -->
          <v-collapse :title="'我是一个下拉面板'">
            <div slot="operate">
              <a href="" class="tbd-link">额外操作</a>
            </div>
            <div style="padding: 20px 0;">
              <p>内容内容</p>
            </div>
          </v-collapse>
          <v-collapse :title="'我是一个下拉面板'">
            <div slot="operate">
              <a href="" class="tbd-link">额外操作</a>
            </div>
            <div style="padding: 20px 0;">
              <p>内容内容</p>
            </div>
          </v-collapse>
          <v-collapse :title="'我是一个下拉面板'">
            <div slot="operate">
              <a href="" class="tbd-link">额外操作</a>
            </div>
            <div style="padding: 20px 0;">
              <p>内容内容</p>
            </div>
          </v-collapse>
        </v-collapse-group>
      </div>

      <h2>步进输入框</h2>
      <div class="doc-example">
        <v-step-input size="small"></v-step-input>
        <v-step-input></v-step-input>
        <v-step-input :size="'large'" :min="10" :max="80" :step="5"></v-step-input>
      </div>

      <h2>进度条</h2>
      <div class="doc-example">
        <v-progress :progress="20"></v-progress>
        <v-progress :size="'large'" :progress="30"></v-progress>
        <v-progress :progress="40" :title="'标题'" :info="'啦啦'"></v-progress>
        <v-progress :progress="40" :is-show-text="true" :is-active="true"></v-progress>
        <v-progress :type="'success'" :progress="50" :explain="'成功'"></v-progress>
        <v-progress :type="'error'" :progress="50" :explain="'失败'"></v-progress>
        <v-progress :type="'warn'" :progress="50" :explain="'警告'"></v-progress>
      </div>

      <h2>加载</h2>
      <div class="doc-example">
        <v-button type="primary" @click="showLoading('Global')">全局loading</v-button>
        <v-button type="primary" @click="showLoading('Part')">局部loading</v-button>

        <v-loading :is-show="showGlobalLoading" :is-global="true" :content="'加载中..'"></v-loading>
        <v-loading :is-show="showPartLoading" :size="'small'"></v-loading>
      </div>

      <h2>步骤条</h2>
      <div class="doc-example">
        <v-steps :data="stepsData"></v-steps>
        <v-steps :data="stepsData" :size="'small'"></v-steps>
        <v-steps :data="stepsData" :is-vertical="true"></v-steps>
      </div>

      <h2>文字提示</h2>
      <div class="doc-example">
        <!-- 底部 -->
        <div style="margin-left: 50px;">
          <div>底部</div>
          <v-tool-tip>文字提示</v-tool-tip>
        </div>

        <div style="margin-left: 50px;">
          <div>底部靠左</div>
          <v-tool-tip :type="'bottomLeft'">文字提示</v-tool-tip>
        </div>

        <div style="margin-left: 50px;">tool-tip
          <div>底部靠右</div>
          <v-tool-tip :type="'bottomRight'">文字提示</v-tool-tip>
        </div>

        <!-- 顶部 -->
        <div style="margin-left: 50px;">
          <div>顶部</div>
          <v-tool-tip :type="'top'">文字提示</v-tool-tip>
        </div>

        <div style="margin-left: 50px;">
          <div>顶部靠右</div>
          <v-tool-tip :type="'topRight'">文字提示</v-tool-tip>
        </div>

        <div style="margin-left: 50px;">
          <div>顶部靠左</div>
          <v-tool-tip :type="'topLeft'">文字提示</v-tool-tip>
        </div>

        <br />
        <!-- 右边 -->
        <div style="margin-left: 50px;">
          <div>右边</div>
          <v-tool-tip :type="'right'">文字提示</v-tool-tip>
        </div>

        <div style="margin-left: 50px;">
          <div>右边靠顶</div>
          <v-tool-tip :type="'rightTop'">文字提示</v-tool-tip>
        </div>

        <div style="margin-left: 50px;">
          <div>右边靠底</div>
          <v-tool-tip :type="'rightBottom'">文字提示</v-tool-tip>
        </div>

        <!-- 左边 -->
        <div style="margin-left: 50px;">
          <div>左边</div>
          <v-tool-tip :type="'left'">文字提示</v-tool-tip>
        </div>

        <div style="margin-left: 50px;">
          <div>左边靠顶</div>
          <v-tool-tip :type="'leftTop'">文字提示</v-tool-tip>
        </div>

        <div style="margin-left: 50px;">
          <div>左边靠底</div>
          <v-tool-tip :type="'leftBottom'">文字提示</v-tool-tip>
        </div>
      </div>

      <h2>时间轴</h2>
      <div class="doc-example">
          <v-time-line :data="timeLineData"></v-time-line>
      </div>

      <h2>标签列表</h2>
      <div class="doc-example">
        <v-tag-list :data="tagList"></v-tag-list>
        <v-tag-list :data="tagList" :size="'small'" :is-delete-able="true"></v-tag-list>
      </div>

      <h2>树形列表</h2>
      <div class="doc-example">
        <v-tree :data="tree"></v-tree>
      </div>

      <h2>穿梭框</h2>
      <div class="doc-example">
        <v-transfer :src-title="'原数据'" :dist-title="'选择'" :data="transfer" :result="transferRes"></v-transfer>
      </div>

      <h2>表单-水平</h2>
      <div class="doc-example">
        <v-form>
          <v-form-item
                  :is-explain-show="true"
                  :explain-text="'输入正确'"
                  :explain-type="'success'"
                  label="账户：">

            <v-input placeholder="请输入账户名" ></v-input>
          </v-form-item>

          <v-form-item
                  label="密码：">
            <v-input type="password" placeholder="请输入密码"></v-input>
          </v-form-item>

          <v-form-item>
            <label className="ant-checkbox-inline">
              <v-checkbox :data="[{label: '记住我', value: true}]"></v-checkbox>
            </label>
          </v-form-item>

          <v-button type="primary">登录</v-button>
        </v-form>
      </div>
      
      <h2>表单-垂直-验证</h2>
      <div class="doc-example">
        <v-form :is-vertical="true" :is-valid="false">
          <v-form-item
                  :is-require="true"
                  :label="'账户：'"
                  :is-explain-show="true"
                  :explain-text="'输入错误'"
                  :explain-type="'error'"
                  :label-col=4
                  :wrapper-col=8>
            <v-input placeholder="请输入账户名" ></input>
          </v-form-item>

          <v-form-item
                  :label="'密码：'"
                  :is-explain-show="true"
                  :explain-text="'输入正确'"
                  :explain-type="'success'"
                  :label-col=4
                  :wrapper-col=8>
            <v-input type="password" placeholder="请输入密码"></input>
          </v-form-item>

          <v-form-item
                  :label="'密码：'"
                  :is-explain-show="true"
                  :explain-text="'警告提示'"
                  :explain-type="'warning'"
                  :label-col=4
                  :wrapper-col=8>
            <v-input placeholder="请输入密码"></input>
          </v-form-item>

          <v-form-item
                  :label="'密码：'"
                  :is-explain-show="true"
                  :explain-text="'验证中提示'"
                  :explain-type="'feedback'"
                  :label-col=4
                  :wrapper-col=8>
            <v-input type="password" placeholder="请输入密码"></input>
          </v-form-item>

          <v-form-item
                  label="选中："
                  label-col=4
                  wrapper-col=4>
            <label className="ant-checkbox-inline">
              <v-checkbox :data="[{label: '记住我', value: true}]"></v-checkbox>
            </label>
          </v-form-item>

          <v-form-item
                  label="多选："
                  label-col=4
                  wrapper-col=4>
            <label className="ant-checkbox-inline">
              <v-checkbox :data="[{label: '我是A', value: true}]"></v-checkbox>
              <v-checkbox :data="[{label: '我是B', value: true}]"></v-checkbox>
              <v-checkbox :data="[{label: '我是C', value: true}]"></v-checkbox>
            </label>
          </v-form-item>

          <v-form-item
                  label="开关："
                  label-col=4
                  wrapper-col=4>
            <label className="ant-checkbox-inline">
              <v-switch></v-switch>
            </label>
          </v-form-item>

          <v-form-item
                  label-col=4
                  wrapper-col=4>
            <v-button :type="'primary'">登录</vButton>
          </v-form-item>
        </v-form>
      </div>

      <h2>搜索框</h2>
      <div class="doc-example">
        {{search}}
        <v-search :value.sync="search" @click.stop="buttonClick"></v-search>
      </div>

      <h2>业务类型组件</h2>
      <h2>编辑表组件</h2>
      <div class="doc-example">
        <v-table-edit :data.sync="tableEdit.data" :types="tableEdit.types"></v-table-edit>
        <br />
        <code>
          {{tableEditResult}}
        </code>
      </div>

      <h2>标签型下拉框</h2>
      <div class="doc-example">
        <v-label-dropdown :data="staff.data"
                          :selected.sync="staff.selected" :disabled="staff.disabled">
        </v-label-dropdown>
      </div>
    </section>

    <div class="doc-footer">
      <p>维护： Zakwu / <a href="mailto:zakwu@tencent.com">email: zakwu@tencent.com</a></p>
    </div>
  </div>
</template>

<script>
  let components = require('./index');


  export default {
    components: components,
    data() {
      return {
        // multi-select
        multiDataList: {
          optsList: (function() {
            var base =[{
              value: 1,
              label: 'value1value1value1value1value1',
              renderLi: function() {
                return `<a>111value1value1value1value1value1</a>`
              }
            }, {
              value: 2,
              label: 'value2disabledvalue2disabled',
              isDisabled: true
            }];

            var other = [];
            for(var i = 0; i < 30; i++) {
              other.push({
                value: i,
                label: 'value' + i
              })
            }

            return base.concat(other);
          })()
        },
        multiResList: [ { "value": 7, "label": "value7" }, { "value": 9, "label": "value9" }, { "value": 17, "label": "value17" }, { "value": 11, "label": "value11" }],
        // tabs
        activeIndex: 2,
        // button group
        buttonGroupList: [{
          text: 'btn1',
          icon: 'android',
          onClick: function() {
            alert('btn1')
          }
        }, {
          text: 'btn2',
          icon: 'apple',
          isSelected: true,
          onClick: function() {
            alert('btn2')
          }
        }, {
          text: 'btn3',
          icon: 'android',
          onClick: function() {
            alert('btn3')
          },
          isDisabled: true
        }],

        // switch
        switchValue: false,

        // checkbox / radio data
        commonListData: [{
          value: 0,
          label: 'value0'
        }, {
          value: 1,
          label: '<a>111</a>'
        }, {
          value: 2,
          label: 'value1',
          isDisabled: true
        }],

        checkboxResultList: [0, '', 2],

        // radio
        radioResultList: [1],
        radioMulResultList: [0, ''],

        // dropdown
        dropDownData: {
          optsList: [{
            value: 0,
            label: 'value0'
          }, {
            value: 1,
            label: 'value1',
            renderLi: function() {
              return `<a>111</a>`
            }
          }, {
            value: 2,
            label: 'value2',
            isDisabled: true
          }]
        },

        dropDownValue: 0,

        // table
        table: {
          data: (function() {
            var res = [];
            for (let i = 0; i < 50; i++) {
              res.push({
                key: i,
                name: `name${i}`,
                age: 32,
                address: `address${i}号`
              });
            }

            return res;
          })(),
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
        },

        // slider
        sliderValue: 10,

        // edit table
        tableEdit: {
          'data': [{
            columnName: 'name',
            columnType: 'string',
            columnDesc: 'init',
            isPartition: true

          }]
        },

        // staff
        staff : {
          data : [
            {userId:1, userName: 'hill'},
            {userId:2, userName: 'shijia'},
            {userId:3, userName: 'zac'},
            {userId:4, userName: 'admin'}
          ],
          selected : [{
            userId : 1,
            userName : 'hill'
          },{
            userId : 2,
            userName : 'shijia'
          }],
          disabled : [{
            userId : 100,
            userName : 'admin'
          }]
        },

        // loading
        showGlobalLoading: false,
        showPartLoading: false,

        // steps
        stepsData: [{
            order: 1,
            title: '完成',
            explain: '说明文字',
            isFinished: true
        }, {
            order: 2,
            title: '进行中',
            explain: '说明文字',
            isActive: true
        }, {
            order: 3,
            title: '默认尺寸',
            explain: '说明文字'
        }],

        // time line
        timeLineData: ['我们发布了alpha \n\r 再试试', '我们发布了beta'],

        // tagList
        tagList: [{
          content: '内容'
        }],
        // 树
        tree: {
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
        },
        // 穿梭框
        transfer: [{
          content: '我是选择框Aaa',
          isChecked: true
        }, {
          content: '我是选择框Bbb'
        }],
        transferRes: [{
          content: '我是选择框Ccc',
          isChecked: true
        }],

        // 搜索框
        search: '',

        // 固定点阵的滑动输入条
        sliderValueList: [{
          label: '0ms',
          value: 0
        }, {
          label: '25ms',
          value: 25
        }, {
          label: '50ms',
          value: 50
        }, {
          label: '100ms',
          value: 100
        }, {
          label: '200ms',
          value: 200
        }, {
          label: '400ms',
          value: 400
        }, {
          label: '1s',
          value: 1000
        }, {
          label: '2s',
          value: 2000
        }],
        sliderValue2: 50
      }
    },

    methods: {
      switchChange(value) {
        console.log('Tab switch result is :', value)
      },

      buttonClick() {
        console.log('u has been click')
      },

      // tips show way 1
      showTips(id) {
        this.$root.$$tips[id].show();
      },

      showTipsWay2() {
        window.Tips.init('tips1', 'info', 'lalalala');

        this.$root.$$tips['tips1'].show();
      },

      // alert
      showAlert(id) {
        this.$root.$$alert[id].show();
      },

      // 展示对话框
      showDialog(id) {
        this.$root.$$dialog[id].show();
      },

      dialogCallbackFn1() {
        alert('ok callback !');
      },

      dialogCallbackFn2() {
        alert('cancel callback !');
      },

      // message box
      showMb(id) {
        this.$root.$$messageBox[id].show();
      },

      showTipsWay2() {
        window.Tips.init('tips1', 'info', 'lalalala');

        this.$root.$$tips['tips1'].show();
      },

      showLoading(value) {
        var _this = this;

        _this['show' + value + 'Loading'] = true;

        setTimeout(function() {
          _this['show' + value + 'Loading'] = false;
        }, 2000);
      }
    },

    ready() {
      // 动态化兼容测试
      const _this = this;
      setTimeout(function() {
        _this.activeIndex = 1;
        // checkbox / radio 测试
        _this.commonListData = [{
          value: 0,
          label: 'value1'
        }, {
          value: 1,
          label: '<a>222</a>'
        }, {
          value: 2,
          label: 'value2',
          isDisabled: true
        }];

        // dropdown
        _this.dropDownData = {
          optsList: [{
            value: 0,
            label: 'change1'
          }, {
            value: 1,
            label: 'change2',
            renderLi: function() {
              return `<a>222</a>`
            }
          }, {
            value: 2,
            label: 'change3',
            isDisabled: true
          }]
        };
      }, 3000);
    }
  }
</script>

<style>
  @charset "UTF-8";

  /* 页面导航 */

  .doc-header ul,
  .doc-header li {
    list-style: none;
  }

  /*==公用菜单==*/

  .doc-header {
    height: 50px;
  }

  .doc-header .inner {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 50px;
    background: #41abe1;
    z-index: 102;
  }

  .doc-header .nav {
    margin: 0 auto;
    padding: 0 30px;
  }

  .doc-header .nav li {
    position: relative;
    float: left;
    *display: inline;
    margin-right: 20px;
    *zoom: 1;
  }

  .doc-header .nav a {
    display: block;
    min-width: 80px;
    text-align: center;
    font: 14px/50px 'Microsoft Yahei';
    color: #fff;
    opacity: 0.6;
    filter: alpha(opacity=60);
    text-decoration: none;
  }

  .doc-header .nav a:hover,
  .doc-header .nav .current a {
    opacity: 1;
    filter: alpha(opacity=100);
    text-decoration: none;
  }

  .doc-header .nav .current:after {
    position: absolute;
    left: 50%;
    bottom: 0;
    margin-left: -4px;
    content: '.';
    width: 0;
    height: 0;
    border-style: solid;
    border-width: 0 5px 6px;
    border-color: #fff transparent;
    font-size: 0;
  }

  .doc-container {
    margin: 20px auto 0;
  }


  /*==首页==*/

  .doc-index {
  }

  .doc-index h1 {
    margin-bottom: 20px;
    font-size: 20px;
    font-weight: bold;
    text-align: center;
  }

  .doc-index .doc-sidebar {
    display: none;
  }

  .doc-index .doc-main {
    margin-left: 0;
    min-height: 500px;
  }

  .doc-index .doc-footer {
    position: static;
    padding: 30px 0;
    width: auto;
    text-align: center;
  }


  /*快速预览*/

  .doc-view {
    position: fixed;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    z-index: 1100;
    background: #fff;
    overflow: hidden;
  }

  .doc-view iframe {
    width: 100%;
    height: 100%;
  }

  .doc-view .nav-bar {
    position: absolute;
    right: -252px;
    top: 5px;
    width: 284px;
    overflow: hidden;
    *zoom: 1;
    -webkit-transition: all 0.5s ease-in;
    -moz-transition: all 0.5s ease-in;
    -ms-transition: all 0.5s ease-in;
    transition: all 0.5s ease-in;
  }

  .doc-view .nav-bar:hover,
  .doc-view .nav-bar.show {
    right: 0;
  }

  .doc-view .links {
    float: left;
  }

  .doc-view .links a {
    display: block;
    margin: 0 -1px -1px 0;
    width: 30px;
    height: 30px;
    border: 1px solid #d1d5d9;
    background: #f4f5f8;
    text-align: center;
    font: 12px/30px 'Microsoft Yahei';
    vertical-align: middle;
  }

  .doc-view .links a:hover {
    text-decoration: none;
    background: #fff;
    color: #383d49;
  }

  .doc-view .links .close {
    font-size: 18px;
  }

  .doc-view .links a:first-child {
    border-top-left-radius: 5px;
  }

  .doc-view .links a:last-child {
    border-bottom-left-radius: 5px;
  }

  .doc-view .nav {
    margin-left: 32px;
    padding: 10px;
    height: 400px;
    background: #f4f5f8;
    border: 1px solid #d1d5d9;
    border-radius: 5px;
    border-top-left-radius: 0;
    box-shadow: 0 0 2px rgba(73, 56, 61, 0.3);
    overflow: auto;
  }

  .doc-view .nav label {
    display: block;
    margin-bottom: 10px;
  }

  .doc-view .nav input {
    margin-top: 3px;
    padding: 4px 10px;
    width: 201px;
    height: 19px;
    border: 1px solid #dee2e5;
    border-color: #bdc4ca #bdc4ca #dee2e5 #dee2e5;
    line-height: 18px;
    font-size: 12px;
  }

  .doc-view .nav h2 {
    margin-bottom: 5px;
    font-weight: bold;
    cursor: pointer;
    opacity: 0.6;
    filter: alpha(opacity=60);
  }

  .doc-view .nav h2.open {
    opacity: 1;
    filter: alpha(opacity=100);
  }

  .doc-view .nav .pages {
    margin: 0 0 5px 10px;
    display: none;
  }

  .doc-view .nav li {
    padding: 3px 0;
  }

  .doc-view .nav a {
    opacity: 0.6;
    filter: alpha(opacity=60);
  }

  .doc-view .nav a:hover {
    opacity: 1;
    filter: alpha(opacity=100);
  }

  .doc-view .nav .current a {
    opacity: 1;
    filter: alpha(opacity=100);
    font-weight: bold;
  }


  /*快速预览——只有导航条*/

  .doc-view.justbar {
    position: static;
    height: 0;
    overflow: visible;
  }

  .doc-view.justbar .nav-bar {
    position: fixed;
    top: 60px;
    z-index: 1002;
  }


  /*==公用ui控件==*/

  .doc-main > h1,
  .doc-main > h2,
  .doc-main > h3,
  .doc-main > h4,
  .doc-main > h5,
  .doc-main > h6 {
    margin-bottom: 20px;
    font-weight: bold;
    color: #222;
  }

  .doc-main > h1 {
    font-size: 26px;
  }

  .doc-main > h2 {
    font-size: 20px;
  }

  .doc-main > p {
    margin-bottom: 10px;
  }

  .doc-main > pre {
    margin-bottom: 20px;
    padding: 8px 15px;
    max-height: 200px;
    background: #f8f8f8;
    border-radius: 5px;
    border: 1px solid #e5e5e5;
    overflow-x: auto;
    font-size: 12px;
    white-space: pre-wrap;
    *white-space: pre;
    word-break: break-all;
  }

  .doc-table {
    width: 100%;
    border-collapse: collapse
  }

  .doc-table th,
  .doc-table td {
    text-align: left;
    padding: 5px 10px;
    border-bottom: 1px solid #e5e5e5
  }

  .doc-table .i-name {
    margin-left: 5px;
  }

  .doc-example {
    margin-bottom: 15px;
    padding: 15px;
    border: 1px solid #ddd;
    border-radius: 4px;
    background: #fff;
    box-shadow: 0 0 10px rgba(56, 61, 73, 0.05);
    *zoom: 1;
  }

  .doc-example-gray-bg {
    background: #e5e9ec;
  }

  .doc-example pre {
    display: block;
    margin: 15px -15px -15px;
  }

  .doc-example pre code {
    margin: 0;
  }

  .doc-example code {
    display: block;
    margin: 15px -15px -15px;
    padding: 10px 20px;
    max-height: 200px;
    background: #fafafc;
    border-radius: 0 0 4px 4px;
    border-top: 1px solid #ddd;
    overflow: auto;
    font-size: 12px;
    white-space: pre-wrap;
    *white-space: pre;
    word-break: break-all;
  }

  .doc-example .doc-part {
    padding: 15px 15px 15px 15px;
    border-bottom: 1px solid #ccc;
  }

  .doc-sidebar {
    position: fixed;
    *left: 20%;
    left: 20px;
    width: 200px;
    max-height: 80%;
    overflow: auto;
  }

  .doc-sidebar-nav {
    margin: 0;
    padding-left: 10px;
    list-style: none;
  }

  .doc-sidebar-nav a {
    display: block;
    padding-left: 20px;
    font:12px/2 'Microsoft Yahei';
    text-decoration: none;
    color: #767676;
  }

  .doc-sidebar-nav a:hover {
    border-left: 1px solid #41abe1;
    padding-left: 19px;
    color: #41abe1;
  }

  .doc-main {
    margin-left: 200px;
    padding: 0 20px;
  }

  .doc-footer {
    position: fixed;
    bottom: 50px;
    width: 260px;
    font-size: 12px;
  }


  /*==公用布局==*/

  .doc-mod {
    margin: 10px auto;
    width: 1260px;
    border: 1px solid #d7dcdf;
    background: #fff;
  }

  .doc-mod > .hd {
    padding: 0 20px;
    height: 46px;
    background: #fafafc;
    border-bottom: 1px solid #e1e5e7;
  }

  .doc-mod > .hd > h2 {
    display: inline;
    font: bold 18px/46px 'Microsoft Yahei';
  }

  .doc-mod > .bd {
    padding: 25px;
    min-height: 120px;
  }


  /*模块分组*/

  .doc-summary {}

  .doc-summary > .hd {
    padding: 0 20px;
    height: 28px;
    border-top: 1px solid #c6cdd3;
    background: #f4f5f8;
  }

  .doc-summary > .hd h3 {
    float: left;
    font: bold 14px/28px 'Microsoft Yahei';
    color: #383838;
  }

  .doc-summary > .bd {
    padding: 10px 0;
  }

  .doc-icons {
    margin: 0 -10px;
    overflow: hidden;
    *zoom: 1;
  }

  .doc-icons li {
    float: left;
    margin: 0 10px 10px;
    width: 150px;
    text-align: center;
    color: #767676;
    border-radius: 5px;
    -webkit-transition: all 0.3s linear;
    transition: all 0.3s linear;
  }
  .doc-icons li:hover {
    background: #41abe1;
    color: #fff;
  }
  .doc-icons li > span {
    display: table-cell;
    width: 150px;
    height: 100px;
    vertical-align: middle;
  }

  .doc-icons .tbdi {
    margin-bottom: 10px;
    font-size: 24px;
  }

  .doc-col-demo {
    padding: 10px;
    border: 1px solid #999;
  }
</style>
