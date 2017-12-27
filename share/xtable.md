# XTable 及Table 组件实现逻辑分享
>先来个简单的XTable案例分析，然后再讲复杂的Table组件实现逻辑


#### XTable 使用


```
	<XTable ajaxUrlName="signCustomers" ajaxParams={this.state.searchParams}>
			<XTableRow label="全选" type="checkbox" name="all" width={30}/>
			<XTableRow label="公司名称" name="signCityName" width={300} tooltip="我的世界"/>
			<XTableRow label="公司" name="company" width={300}/>
			<XTableRow label="时间" name="receiveTimey" type="date" width={100}/>
			<XTableRow label="时间" name="createDate" type="date" width={200}/>
			<XTableRow label="操作" type="operation" component={(scope)=>{
					return <Button onClick={this.onClick} label={scope.signCityName} type="button"/>;
				}} />
	</XTable>

```

XTable相关参数

|属性|含义|默认值|
|----|----:|----:|
|ajaxUrlName|请求url别名看api config文件定义|demo|
|ajaxParams|搜索参数|{}|
|ajaxFieldListName|列表字段读取|'items'|
|page|当前分页|1|
|pageSize|列表显示条数|20|
|ajaxParams|搜索参数|{}|
|onLoaded|已经渲染| |
| onExport | 导出 | function|


XTableRow

|属性|含义|默认值|
|----|----:|----:|
|name|字段名称| |
|type|checkbox、date||
|component|渲染时用到的dom||
|defaultValue|默认值||
|width|每列的宽度||
|tooltip|hover显示的内容,可以是string、function| function |



#### XTable组件直接上代码～


