# 10 XMSC_Code_08_收货地址的实现
## 10.1	任务描述
### 10.1.1 任务介绍
实现收货地址的添加、修改和删除等功能。
### 10.1.2	任务要求
* 参考小米网站，实现收货地址界面。
* 一行最多放三个地址，左边第一列放添加新地址
* 点击左边的添加新地址，弹出模态框添加数据。除了标签其他数据都必填，姓名和手机号码参考之前任务中的验证，邮政编码6位数字（更详细的验证要求请自行百度）。选择省/市/区/街道，改为三个select（省/市/区）。数据放在json文件中（自行编写数据），需实现三个下拉框之间的联动。保存后，页面添加一条收货地址数据。
* 在某项收货地址上点击修改，弹出模态框修改数据。
* 删除和修改数据后记得更新页面。
* 在某项收货地址上点击删除，询问用户是否要删除，确认后再删除。用自定义的模态框代替confirm函数
* 感兴趣的同学可以使用本地存储存放收货地址数据。
## 10.2 具体需求
字段 | 说明 | 来源
:----|:-----:|-----:

| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |

## 10.2	工作指导说明
    用户在个人中心页面，选个人中心菜单→收货地址菜单进入收货地址管理页面。
### 10.2.1 页面初始化
1. 声明一个数组存放收货地址数据
```javascript
var ADDRESS_KEY = 'Address';
var addresses = store.get(ADDRESS_KEY,[]);
//生成地址列表
function makeAddressList(addresses){
  var html = '';
  for(var i = 0, len = addresses.length; i < len; i++){
    html += makeAddressItem(addresses[i]);生成
  }
  $('#addressList').append(html);
}
//生成地址详情
function makeAddressItem(address){
  var html = '';
  //......
  return html;
}
makeAddressList(addresses);
//添加按钮的click事件处理
$('#').on('click', function(){
});
```
2、	每条收货地址数据用object类型，包含：id、姓名、手机号、省、市、区、详细地址、邮政编码和标签等属性。
3、	显示收货地址时需要把收货地址相关属性的值拼接在一起。
## 10.3	工作产品要求
收货地址的界面参考如下：
