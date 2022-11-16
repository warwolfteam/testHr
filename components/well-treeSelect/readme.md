更新参数说明日志

效果：
[点击链接](https://vkceyugu.cdn.bspapp.com/VKCEYUGU-aliyun-qipsksoswcfp9547ba/206f1be0-5325-11eb-a16f-5b3e54966275.mp4)
<video src="https://vkceyugu.cdn.bspapp.com/VKCEYUGU-aliyun-qipsksoswcfp9547ba/206f1be0-5325-11eb-a16f-5b3e54966275.mp4" width="800px" height="600px" controls="controls"></video>

# 使用

引入：
```
<well-tree-select @doConfirm="doConfirmCategorys"
                  :showDialog.sync="showDialog"
                  :data="categorysList"
                  :title-text="'选择职位'"
                  :max-selected="2"
                  :selected-ids="selectedIds">
</well-tree-select>
```
参数说明
<table>
  <tr>
    <th>参数</th>
    <th>说明</th>
    <th>例子</th>
  </tr>
  <tr>
    <td>showDialog</td>
    <td>显示组件，Boolean，默认false</td>
    <td>true</td>
  </tr>
  <tr>
      <td>titleText</td>
      <td>组件标题</td>
      <td>'请选择'</td>
    </tr>
  <tr>
    <td>maxSelected</td>
    <td>最多选中几项，Number，默认3 </td>
    <td>1</td>
  </tr>
  <tr>
    <td>selectedValues</td>
    <td>选中的值的value，Array，[] </td>
    <td>[060ef5006a504697a7d642d7e7d199cc', '060ef5006a504697a7d642d7e7d199cc']</td>
  </tr>
  <tr>
    <td>data</td>
    <td>数据列表，Array，默认[] </td>
    <td>
<pre>
<code>
[{
    "label": "技术",
     "children": [
       {
         "label": "后端开发"
         "children": [
            {
             value: '060ef5006a504697a7d642d7e7d199cc',
              label: 'Java'
            },
            {
              value: '060ef5006a504697a7d642d7e7d199cc',
              label: 'Java'
          }]
       }]
    }]
</code>
</pre>
    </td>
  </tr>
  <tr>
    <td>@clickNav</td>
    <td>点击一级标签时触发的事件</td>
    <td>-</td>
  </tr>
  <tr>
    <td>@clickSub</td>
    <td>点击二级标签时触发的事件</td>
    <td>-</td>
  </tr>
  <tr>
    <td>@clickThird</td>
    <td>点击三级标签时触发的事件</td>
    <td>-</td>
  </tr>  
  <tr>
    <td>@doConfirm</td>
    <td>点击确定时触发的事件</td>
    <td>-</td>
  </tr>
</table>


